## Why am I using this Hashnode blog as a portfolio site?

I've been trying to put together a portfolio site since I completed my [Le Wagon](https://www.lewagon.com/) bootcamp, and threw together a basic [Github Pages](https://pelicularities.github.io/portfolio-lw/) one-page thing as a temporary measure. However, I knew I wanted to transition to a more permanent, more comprehensive professional website as soon as I could, so I sat down and mapped out what I could do with a portfolio site.

First, I did what my instincts told me to do: I thought about what information I wanted to display on my portfolio site, and built an overly-rich data model for the 12 million projects I didn't have but imagined that I would someday build using a multitude of languages and frameworks:

![Whimsical DB schema.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605949032614/frHr_p1St.png)

The idea I had was that a visitor could click on a tag or a dropdown, and see all the projects I'd built using a particular framework or programming language.

![Whimsical wireframe.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605949059859/X_Se7la2B.png)

Once I'd cleaned up my bootcamp projects enough to start building a proper portfolio site, I got to work. I generated my models and wrote my migrations. I even wrote a seed to populate my database with three projects. I mean, if you want to see how far along I got, you can look at the [github repository](https://github.com/pelicularities/portfolio-old) for a Rails-based CRUD portfolio site with a grand total of three projects to show off.

The next step was to turn my wireframe into HTML and CSS, and here is where I fell down hard. My wireframe had nine projects on the index page, but in reality, I had only three projects to show:

![Portfolio old design.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605949342570/UfcQtEaa3.png)

Well, that just looks sad, doesn't it?

Even better, all three projects were Rails and Bootstrap projects. [Rent-a-Pokemon](/rent-a-pokemon) used vanilla JavaScript and [Macrotery](/macrotery) used StimulusJS, but that was it — hardly a ringing endorsement of the vast range of my skills.

## An aside: going deep rather than broad

My initial post-bootcamp plan was to learn React using Le Wagon's and [Frontend Masters'](https://frontendmasters.com/) React courses, then complete [CS50x Web](https://cs50.harvard.edu/web/2020/) (stack: Django, PostgreSQL, React), then get a [Laracasts](https://laracasts.com/) subscription and learn Laravel, then find some resource or another and build something using the MEAN stack and learn MongoDB, Express.js, Angular and Node.js that way. Great plan!

Fortunately, I read Endy Austin's excellent article on FreeCodeCamp: [What I Wish I Knew as a Junior Dev — Lessons Learnt After 11 Years of Coding](https://www.freecodecamp.org/news/lessons-learned-after-11-years-coding/). The lesson that jumped out at me was "Master one thing":

> New developers tend to jump around learning a lot of things...

> You learned React for one week. Then JavaScript for two weeks. Laravel for three.

> **Stop.**

> You need to wake up and realize that you’re simply extending the time it’ll take you to truly learn anything.

> Pick one thing.

> Stick with it for a few months – ideally 6 to 12 months before you move to something else.

> This has two benefits:
> 1. You’ll go deep enough and hit critical mass that moves you towards mastery.
> 2. After you master one domain, you can transfer knowledge to another.

It wasn't what I wanted to hear, but it was what I needed to hear. I decided to focus on learning Rails and JavaScript as thoroughly as I could, instead of trying to take in everything all at once.

This had a major implication for my original portfolio idea: it meant that the message I was trying to send, that I could learn a lot of skills in a short amount of time, was no longer relevant. Instead, I needed to demonstrate an ability to learn *deeply* in a short amount of time.

# Back to the product problem

So now I was stuck: I had very few projects, and needed to think about how to showcase them as best as I could. This looked like a design problem, but it is in fact a *product* problem: I was building a product to showcase my skills, and there was a mismatch between what the product could showcase and what my skills were.

I've always been more inclined towards back-end development. Going through the Le Wagon bootcamp gave me a great appreciation for front-end work and made me determined to improve my front-end skills, but it is not my natural happy place (not yet). In hindsight, it's completely understandable why my first instinct was to sit down and draw a database schema: I gravitated to my strongest suit.

If I were more comfortable with front-end development, I would probably front-end-developed my way out of the design problem: foregrounded the projects instead of hiding each one behind a layer of CRUD, built a carousel of thumbnails, added CSS transitions. After all, it would have been a great way to show off my development skills. Unfortunately, all I did was show off my ability to create rich back-end models for data that didn't exist.

I stopped and thought, is this the best way to display what I'm capable of, and where my strengths lie?

Clearly not. I needed to outsource the design, and find a way to build a professional site that puts my computational thinking and technical communication skills front and centre.

# Portfolio as process

A couple of weeks before I got stuck on this portfolio problem, I had created a [Hashnode](https://hashnode.com/) account. I had the vague idea that I would blog about my journey to learn everything I could about software development, but I didn't have a clue where to start.

Now, thinking through what my portfolio should look like, I put two and two together: *my portfolio site should be a Hashnode blog*.

This way, I could not just showcase my projects, but *discuss* them: what shaped the project planning and outcomes, why certain software design decisions were made, what I learnt on each project. As a very junior developer, my portfolio does not and cannot take the form of stone tablets descending from Mount Sinai, a fait accompli from the heavens. Instead, what I have to offer, and what I can share freely with others is *my own growth as a developer*.

That's why I've chosen to make my portfolio a blog, and my blog a portfolio.

It doesn't mean that I won't try to code my own portfolio site in the future — I almost certainly will, if only to have a playground to experiment and push my skills further. (Hmm, in fact, maybe I should put together a "code playground" site — there's an idea.) For now, though, I think this is the best way to record what I've learnt and what I'm capable of as a software developer.

I hope you enjoy what you read here, and stick around for a while.