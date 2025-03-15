For the initial project structure you are going to create it in the components folder because this local search bar for this project will be used in multiple places
Based on [[URL State management]]
Hooks usedL
useSearchParams() =>
![[Pasted image 20250111165725.png]]

Using query-string lirbary 
![[Pasted image 20250111200718.png]]
makes it easier to work with url queries

```tsx
const router = useRouter()
router.push(newUrl, { scroll: false })

    const pathname = usePathname()
    
     const searchParams = useSearchParams()

    const query = searchParams.get("query") || ""

    const [searchQuery, setSearchQuery] = useState(query)

    useEffect(() => {

        if (searchQuery) {

            // params: searchParams.toString() this is to get the Existing key value

            // pairsand the following parameterswill be for passing the new key value pairs

            const newUrl = formUrlQuery({ params: searchParams.toString(), key: "query", value: searchQuery });

            router.push(newUrl, { scroll: false })

        }
```
Both hooks are from next navigation the router dot push is used to navigate to the new url, pathname returns the current url

Debouncing the requests: LocalSearch

```tsx
"use client"

import React, { useEffect, useState } from 'react'

import Image from "next/image";

  

import { Input } from "../ui/input";

import { usePathname, useRouter, useSearchParams } from 'next/navigation';

import { formUrlQuery, removeKeysFromUrlQuery } from '@/lib/url';

interface Props {

    route: string;

    imgSrc: string;

    placeholder: string;

    otherClasses?: string;

}

const LocalSearch = ({ route, imgSrc, placeholder, otherClasses }: Props) => {

    const router = useRouter()

    const pathname = usePathname()

    const searchParams = useSearchParams()

    const query = searchParams.get("query") || ""

    const [searchQuery, setSearchQuery] = useState(query)

    useEffect(() => {

        console.log(pathname, "pathname")

        const debounce = setTimeout(() => {

            if (searchQuery) {

                const newUrl = formUrlQuery({

                    params: searchParams.toString(),

                    key: "query",

                    value: searchQuery,

                });

  

                router.push(newUrl, { scroll: false });

            } else {

                if (pathname === route) {

                    const newUrl = removeKeysFromUrlQuery({

                        params: searchParams.toString(),

                        keysToRemove: ["query"],

                    });

  

                    router.push(newUrl, { scroll: false });

                }

            }

        }, 1000)

        return () => {

            clearTimeout(debounce)

        }

    }, [searchQuery, route, router, searchParams, pathname])

    return (

        <div

            className={`background-light800_darkgradient flex min-h-[56px] grow items-center gap-4 rounded-[10px] px-4 ${otherClasses}`}

        >

            <Image

                src={imgSrc}

                width={24}

                height={24}

                alt="Search"

                className="cursor-pointer"

            />

            <Input

                type="text"

                placeholder={placeholder}

                value={searchQuery}

                onChange={(e) => setSearchQuery(e.target.value)}

                className="paragraph-regular no-focus placeholder text-dark400_light700 border-none shadow-none outline-none"

            />

        </div>

    );

};

  

export default LocalSearch;
```



	Using the search in main home page (lecture local search bar))
```tsx
import Link from "next/link";

  

import LocalSearch from "@/components/search/LocalSearch";

import { Button } from "@/components/ui/button";

import ROUTES from "@/constants/routes";

  

const questions = [

  {

    _id: "1",

    title: "How to learn React?",

    description: "I want to learn React, can anyone help me?",

    tags: [

      { _id: "1", name: "React" },

      { _id: "2", name: "JavaScript" },

    ],

    author: { _id: "1", name: "John Doe" },

    upvotes: 10,

    answers: 5,

    views: 100,

    createdAt: new Date(),

  },

  {

    _id: "2",

    title: "How to learn JavaScript?",

    description: "I want to learn JavaScript, can anyone help me?",

    tags: [

      { _id: "1", name: "React" },

      { _id: "2", name: "JavaScript" },

    ],

    author: { _id: "1", name: "John Doe" },

    upvotes: 10,

    answers: 5,

    views: 100,

    createdAt: new Date(),

  },

];

  

interface SearchParams {

  searchParams: Promise<{ [key: string]: string }>;

}

  

const Home = async ({ searchParams }: SearchParams) => {

  const { query = "" } = await searchParams;

  

  const filteredQuestions = questions.filter((question) =>

    question.title.toLowerCase().includes(query?.toLowerCase())

  );

  

  return (

    <>

      <section className="flex w-full flex-col-reverse justify-between gap-4 sm:flex-row sm:items-center">

        <h1 className="h1-bold text-dark100_light900">All Questions</h1>

  

        <Button

          className="primary-gradient min-h-[46px] px-4 py-3 !text-light-900"

          asChild

        >

          <Link href={ROUTES.ASK_QUESTION}>Ask a Question</Link>

        </Button>

      </section>

      <section className="mt-11">

        <LocalSearch

          route="/"

          imgSrc="/icons/search.svg"

          placeholder="Search questions..."

          otherClasses="flex-1"

        />

      </section>

      {/* HomeFilter */}

      <div className="mt-10 flex w-full flex-col gap-6">

        {filteredQuestions.map((question) => (

          <h1 key={question._id}>{question.title}</h1>

        ))}

      </div>

    </>

  );

};

  

export default Home;
```