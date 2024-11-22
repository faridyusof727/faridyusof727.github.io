+++
date = '2024-11-22T22:08:02+08:00'
title = 'Sentinel Error'
+++

I was working on a project where I need to check on certain errors that return
from a deep, deep function.

The deepest function was calling a third party API. Fortunately, the third party
package that I was using is pretty following 'single responsibility principle'.

Ah, this is great! Since the function purpose is to wait until some capacity is
ready on the provider side, I can just check on the error the function returns.

Below is the current implementation before I refactor it.

```go
someWaitingProcess, err := provider.WaitUntilReady()
if err != nil {
    return err
}
```

In my thought process, I knew that the error is related to problem waiting for
capacity. However, I can't return the error directly.

On the upper layer, I need to check on the error and return a specific error, but
I can't just do something like below:

```go
theFunc, err := functionThatCallsWaitUntilReady()
if err != nil {
    if err.Error() == "wait until ready error" {
        // handle the error
    }

    return err
}
```

Why? There's a possibility that the error returned from the deepest function is
being changed by the third party package. Possible!

The easiest way to handle this is to create a sentinel error.

```go
var ErrWaitUntilReady = errors.New("wait until ready error")

someWaitingProcess, err := provider.WaitUntilReady()
if err != nil {
    return ErrWaitUntilReady
}
```

Now, I can refactor the code to something like below:

```go
someWaitingProcess, err := provider.WaitUntilReady()
if err != nil {
    if errors.Is(err, ErrWaitUntilReady) {
        // handle the error
    }
}
```

I think this is a good way to handle this kind of problem.

If this is helpful, feel free to share it with others. Just writing it down so
I won't forget. 😃😃😃
