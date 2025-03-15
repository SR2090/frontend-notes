

```tsx
"use client"

import React, { useState } from 'react'

import { Button } from '../ui/button';

import { formUrlQuery, removeKeysFromUrlQuery } from '@/lib/url';

import { useRouter, useSearchParams } from 'next/navigation';

import { cn } from '@/lib/utils';

const filters = [

    { name: "Newest", value: "newest" },

    { name: "Popular", value: "popular" },

    { name: "Unanswered", value: "unanswered" },

    { name: "Recommeded", value: "recommended" },

];

  

const HomeFilter = () => {

  

    const searchParams = useSearchParams();

    const query = searchParams.get("filter") || "";

    const [active, setActive] = useState(query || "")

    const router = useRouter()

    const handleTypeClick = (filterValue: string) => {

        if (active === filterValue) {

            setActive("");

            const newUrl = removeKeysFromUrlQuery({

                params: searchParams.toString(),

                keysToRemove: ["filter"],

            })

            console.log('newUrl', newUrl)

            router.push(newUrl, { scroll: false });

        } else {

            setActive(filterValue);

            const newUrl = formUrlQuery({

                params: searchParams.toString(),

                key: "filter",

                value: filterValue.toLowerCase(),

            })

            router.push(newUrl, { scroll: false });

        }

    }

    return (

        <div className='mt-10 hidden flex-wrap gap-3 sm:flex'>

            {filters?.map((filter) => {

                return (<Button key={filter?.name} className={cn(

                    `body-medium rounded-lg px-6 py-3 capitalize shadow-none`,

                    active === filter.value

                        ? "bg-primary-100 text-primary-500 hover:bg-primary-100 dark:bg-dark-400 dark:text-primary-500 dark:hover:bg-dark-400"

                        : "bg-light-800 text-light-500 hover:bg-light-800 dark:bg-dark-300 dark:text-light-500 dark:hover:bg-dark-300"

                )}

                    onClick={() => handleTypeClick(filter.value)}>

                    {filter?.name}

                </Button>)

            })}

        </div >

    )

}

  

export default HomeFilter
```



Accessing the filter value in home page
