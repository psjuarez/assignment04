# A4 Write-up

**Name: Paul Juarez**
**Onyen: psjuarez**
**Game URL:** https://bridges-cs.herokuapp.com/assignments/4/
**Bomb rule I played with (SHRINK or GAME_OVER):Shrink Implementation**

Three questions, 20 points. A few sentences each. Where a question asks for a
number, show where it came from.

---

## Question 1: The tail pointer (7 points)

Your `LinkedQueue` keeps a `tail` reference. Suppose you deleted it and found
the back of the queue by starting at `head` and following `next` until you ran
out of nodes.

What would `enqueue` cost then, in Big-O? The game calls `enqueue` once per
tick and runs about 7 ticks a second. For a snake 500 cells long, roughly how
many nodes would `enqueue` alone visit each second, and would you notice?

Now do the same for the autograder's speed test. It fills a queue with
400,000 items, then does 400,000 more rounds of dequeue-then-enqueue, so the
queue stays at 400,000. Roughly how many nodes would those enqueues visit?

```
In this case where you need to find the back of the
queue manually, it would need to go through n items,
so Big-O would be O(n).
If the game is forcing itself to scan through
500 cells every tick, that would mean there are
3500 cells being run through every second, which
would likely be unnoticeable?
However, if it's forcing itself to run through
400,000 items 400,000 times, the game would need to
run through like 1.6 billion cells.
```

---

## Question 2: The one method allowed to walk (7 points)

`contains` is O(n), and the game calls it through `snake.occupies(...)`. Read
`GameState.tick()` and `GameState.freeCell()` and find every call.

On a tick where the snake eats an apple, roughly how many nodes do those
`contains` calls visit in total, for a snake of length n on the 30 by 30
board? Give an expression in n. Then name a data structure from later in this
course that would make "is the snake on this cell?" fast, and say what it
would cost to keep it up to date as the snake moves.

```
A few things need to happen after an apple is eaten.
First, the constant snake.occupies(next) is run which
runs through up to n options.
Then since an apple is eaten, it also needs to
figure out all the free cells that the next apple and
bombs can spawn in. This runs up to 900n checks.
Therefore, it is n + 900n cells that are checked.

A future data structure could be a hash set, for
quick computation. Because the computation is O(1)
```

---

## Question 3: Which end is the head? (6 points)

The snake's head is the **back** of the queue, and its tail end is the
**front**. Explain why, using what happens to the body on each tick.

Then suppose you flipped it, so the head was the front. Which operation would
each tick need that `LinkedQueue` does not have, and why is that operation hard
to make O(1) on a singly linked list?

```
Because the front of the queue gets removed through
dequeue(), and the snake in the game gets its tail
removed every tick, it only makes sense to associate
the front of the queue with the tail of the snake.
the back of the queue has stuff added to it, just like
the head of the snake.

it's very hard to remove the end of the list, because
you usually need to travel all the way to the end
to remove it. So it makes sense to be unflipped.
```
