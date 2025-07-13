+++
date = '2025-07-13T08:58:32+08:00'
title = 'Start Simple With Go'
+++

You know, Go (or Golang, as some people call it) is known for its simplicity.
But as your project grows, things won't stay simple forever.

You can still maintain simplicity in your code organisation.
How you structure your codebase really depends on your approach.
Some developers start encapsulating things immediately, while others prefer to
keep it simple at first.

When you start structuring your codebase, you might be biased-especially
if you're coming from a different ecosystem or programming "tribe."
Your structures are probably influenced by those other languages.

A common example that I noticed:

```shell
.
└── Root Project/
    ├── handlers/
    │   └── user/
    │       └── handler.go
    └── repositories/
        ├── user/
        │   └── repository.go
        ├── business/
        │   └── repository.go
        └── payment/
            └── repository.go
```

Go code is known for its simplicity and "flatness." The Go community intentionally
avoids deep folder structures, unnecessary abstractions, and generic naming.
Idiomatic Go code is about clarity, discoverability, and minimal ceremony.

As the project grows, maintaining that folder structure becomes a headache.
In my experience, you'll have a hard time navigating the codebase.

## So, what's best?

Now, I hear some of you might hearing screaming a very useful rule of thumb
(or even proverb, if you will): "Flat until hurts!". The proverb explains,
in Go, it's pretty common to have flatter version of the folder structure, and,
until it hurts. When the structure becomes harder to navigate or even to maintain,
that would be the correct time to start refactoring.

> The advice I find myself repeating is to prefer fewer, larger packages.
> Your default position should be to not create a new package. That will
> lead to too many types being made public creating a wide, shallow,
> API surface for your package.
>
> Link: <https://dave.cheney.net/practical-go/presentations/qcon-china.html#_consider_fewer_larger_packages>
>
> -- [Dave Cheney](https://dave.cheney.net/about)

Refactoring, or I would say, enhancing the structure would be a simple task to do.

Now, let us fix the above to more an idiomatic structuring.

```shell
.
└── Root Project/
    ├── user // Notice this is the only `package` we've created
    │   ├── repository.go 
    │   ├── handler.go
    │   └── service.go
    ├── business/
    │   └── repository.go
    └── payment/
        └── repository.go
```

**Separation by Domain**: Splitting repositories into folders like `user/`,
`business/`, and `payment/` does help keep domain logic isolated.
That's good if you care about boundaries and avoiding giant "everything" folders.

## When you start hurting

Let say your project grows even further. And now, you might probably have something
like this:

```shell
.
└── Root Project/
    ├── user/
    │   ├── profile_repository.go
    │   ├── password_repository.go
    │   ├── notification_repository.go
    │   ├── avatar_repository.go
    │   ├── handler.go
    │   └── service.go
    ├── business/
    │   └── repository.go
    └── payment/
        └── repository.go
```

Go makes it easy to refactor and you can extract shared concerns. As for example,
you can move shared logic (e.g., notifications, emails, events, utils) into
their own top-level packages:

```shell
.
└── Root Project/
    ├── user/
    │   ├── repository.go
    │   ├── handler.go
    │   ├── service.go
    │   └── profile/ // Profile only relates to `user`
    │       ├── repository.go
    │       └── service.go
    ├── notification/ // Notification could be a general package
    │   ├── repository.go
    │   └── service.go
    ├── business/
    │   └── repository.go
    └── payment/
        └── repository.go
```

The point that I'm trying to emphasise is, to always "start simple". Your structure
is totally fine… until it isn't. As soon as files/domains start to balloon or
cross-cutting concerns emerge, refactor by subdomain/feature and move shared
concerns out to their own packages.

That's exactly what mature Go projects do-don't wait until you're in pain to start!
