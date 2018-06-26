---
title: "Coin Flip Probability with Go"
date: 2018-06-25T22:51:22-05:00
draft: true
---

I decided to return to this problem of average probability of getting two heads flipped in a row versus a heads then a tails. I know, beat a dead horse much (💀🐴)? Hear me out...

Sadly, our 100 year old oak in the front yard is slowly dying, which means that for the majority of the day today, I didn't have electricity...and electricity causes internet, which means that I also didn't have internet. I know, I could have gone to a coffee shop, campus, hacked into my neighbors' "toolshed" network, but here's the thing, taking down an oak tree makes a lot of noise. I have 2 dogs and one we suspect had quite an abusive past and her and loud noises...well...let's just say she can't deal. 

In an effort to keep them comfortable, I stayed home. It was a good opportunity for me to take the offline tutorials to learn `go`. I've been meaning to do so because it's fast and the logo is really cute.

![Go Logo](/img/post5/go_logo.png)

So I thought this would be a good learning experience. The tutorials are great but this problem is a good way to start thinking about the language. If you need a refresher of what I am talking about, [here's](https://jcbain.github.io/blog/coin-flip-probs/) my post about it in `python`. 

{{< tweet 1008939111925809153 >}}

Keep in mind I am still learning here, so there's most certainly a more elegant solution but here we go...step by step. 

Step 1: Load in packages

```go
package main

import (
        "fmt"
        "math/rand"
        "time"
        "reflect"
)
```
I'm going to say one thing here; I really like how it throws an error when I don't use a package that I load in.

Step 2: Write a function to simulate a coin flip:

```go
// simulate flipping a fair coin
func FlipCoin() string {
        rand.Seed(time.Now().UnixNano())

        if flipint := rand.Intn(2); flipint == 0 {
               return "tails"
        }
        return "heads"
}
```

The `rand` package provides some pretty convenient methods, however, they are deterministic by default and therefore setting the seed is important. I know, seed setting makes it deterministic too, which is why I followed the convention of passing the current nanosecond as the seed. `rand.Intn(2)` also returns either 0 or 1. Perfect!

Step 3: Flip until condition is met.

```go
// flip until condition is met
func FlipCondition() int {
        flips    := [2]string{FlipCoin(), FlipCoin()}
        previous := 0
        current  := 1
        s        := flips[previous: current+1]
        cond     := []string{"heads","tails"}
        numflips := 2

        for !reflect.DeepEqual(s, cond) {
                s[previous] = s[current]
                s[current] = FlipCoin()
                numflips +=1
        }
        return numflips
}
```

In this function, it is currently set to stop whenever it finds heads and then tails. 


Step 4: Run many trials and return a slice.

```go
// run multiple trials
func FlippityFlip(numtrials int) []int {
        vals := make([]int, numtrials)
        for i := 0; i < numtrials; i++ {
                vals[i] = FlipCondition()
        }
        return vals
}
```

This simply runs `FlipCondition()` `numtrials` times and saves it in a slice.

Step 5: Implement a function to find the mean.

```go

// mean function
func mean(vals[]int) float64 {
        tot := 0.0
        for _, v := range vals{
                tot += float64(v)
        }
        return tot/float64(len(vals))
}
```

Step 6: Wrap it all together and find the average in the `main()` function.

```go
func main() {
        trials := FlippityFlip(10000)
        fmt.Println(mean(trials))
}
```

This runs it 10,000 times and then calculates the average. The final step is to make my way over to a terminal and run the `go run` command on this file to assess the output.


For heads then tails: 

```bash
go run coinflip.go
4.0054
```


For heads then heads:
```bash
go run coinflip.go
5.9916
```

It still works! You know, the great thing about this exercises is that I knew what to expect. This served as a sort of check on my code since, you know, I'm new to all of this...

Oh, if you want to take a look at the code it [right here](https://github.com/jcbain/coinflipgo).