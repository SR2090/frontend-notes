```tsx
import Image from "next/image";

import Link from "next/link";

import React from "react";

  

interface Props {

    imgUrl: string;

    alt: string;

    value: string | number;

    title: string;

    href?: string;

    textStyles: string;

    imgStyles?: string;

    isAuthor?: boolean;

}

  

const Metric = ({

    imgUrl,

    alt,

    value,

    title,

    href,

    textStyles,

    imgStyles,

    isAuthor,

}: Props) => {

    const metricContent = (

        <>

            <Image

                src={imgUrl}

                width={16}

                height={16}

                alt={alt}

                className={`rounded-full object-contain ${imgStyles}`}

            />

  

            <p className={`${textStyles} flex items-center gap-1`}>

                {value}

  

                <span

                    className={`small-regular line-clamp-1 ${isAuthor ? "max-sm:hidden" : ""}`}

                >

                    {title}

                </span>

            </p>

        </>

    );

  

    return href ? (

        <Link href={href} className="flex-center gap-1">

            {metricContent}

        </Link>

    ) : (

        <div className="flex-center gap-1">{metricContent}</div>

    );

};

  

export default Metric;
```
![[Pasted image 20250112183154.png]]

Usage of the metric component

```tsx
import Link from "next/link";

import React from "react";

  

import ROUTES from "@/constants/routes";

import { getTimeStamp } from "@/lib/utils";

  

import TagCard from "./TagCard";

import Metric from "../Metric";

  

interface Props {

    question: Question;

}

  

const QuestionCard = ({

    question: { _id, title, tags, author, createdAt, upvotes, answers, views },

}: Props) => {

    return (

        <div className="card-wrapper rounded-[10px] p-9 sm:px-11">

            <div className="flex flex-col-reverse items-start justify-between gap-5 sm:flex-row">

                <div>

                    <span className="subtle-regular text-dark400_light700 line-clamp-1 flex sm:hidden">

                        {getTimeStamp(createdAt)}

                    </span>

  

                    <Link href={ROUTES.QUESTION(_id)}>

                        <h3 className="sm:h3-semibold base-semibold text-dark200_light900 line-clamp-1 flex-1">

                            {title}

                        </h3>

                    </Link>

                </div>

            </div>

  

            <div className="mt-3.5 flex w-full flex-wrap gap-2">

                {tags.map((tag: Tag) => (

                    <TagCard key={tag._id} _id={tag._id} name={tag.name} compact />

                ))}

            </div>

  

            <div className="flex-between mt-6 w-full flex-wrap gap-3">

                <Metric

                    imgUrl={author.image}

                    alt={author.name}

                    value={author.name}

                    title={`• asked ${getTimeStamp(createdAt)}`}

                    href={ROUTES.PROFILE(author._id)}

                    textStyles="body-medium text-dark400_light700"

                    isAuthor

                />

  

                <div className="flex items-center gap-3 max-sm:flex-wrap max-sm:justify-start">

                    <Metric

                        imgUrl="/icons/like.svg"

                        alt="like"

                        value={upvotes}

                        title=" Votes"

                        textStyles="small-medium text-dark400_light800"

                    />

                    <Metric

                        imgUrl="/icons/message.svg"

                        alt="answers"

                        value={answers}

                        title=" Answers"

                        textStyles="small-medium text-dark400_light800"

                    />

                    <Metric

                        imgUrl="/icons/eye.svg"

                        alt="views"

                        value={views}

                        title=" Views"

                        textStyles="small-medium text-dark400_light800"

                    />

                </div>

            </div>

        </div>

    );

};

  

export default QuestionCard;
```
