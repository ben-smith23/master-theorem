# Lab: Master Theorem

Notice that this lab is not hosted on github but on a competitor website gitlab.
There are many different websites for hosting git repositories,
but all of them are just front-ends for the git command line utility.
We are using github in class because it provides a convenient and free continuous integration system (github actions) for open source projects,
so you don't have to pay every time you submit an assignment and run the test cases.

The purpose of this lab is to both get you familiar with using these non-github webpages, and to practice the master theorem.

## Tasks

1. Clone this repo on to the lambda server.

    > **NOTE:**
    > I'm not going to give you the exact command to run in these instructions because that's a gauche thing to do.
    > Real world instructions often assume you are capable of figuring out these sorts of details for yourself.
    > The command will look like the clone commands you've been running before, just with a gitlab.com url instead of a github.com url.
    > (I am of course happy to answer any questions if you can't get this to work.)

1. Now you will practice using the master theorem.

    The file `search.py` contains three functions.
    Run the doctests to ensure that they are implmented correctly.

    > **NOTE:**
    > Running doctests should become a habit for you on every new python file you see.
    > Again, I'm not going to give you the command because that's uncouth.
    > The exact commands can vary slightly from system to system,
    > and so library/tutorial authors usually assume you'll be able to figure out these details yourself.
    > I want you to get some practice figuring out things things for yourself,
    > but I am of course happy to answer any questions if you can't get this to work.

    The first two functions in `search.py` are the sequential search and binary search algorithms you saw last week.

    Recall that the sequential search had a worst case runtime of $\Theta(n)$.

    > **NOTE:**
    > I'm being careful to state that this was a *worst case runtime* of $\Theta(n)$.
    > The *best case runtime* happens when `xs[0] == y`,
    > and the runtime is then $\Theta(1)$ regardless of the size of the input list `xs`.
    > When we talk about just the *runtime* without a qualifer,
    > then this includes all possible cases.
    > There is no $\Theta$ bound that can hold for both cases,
    > and so the best statement that we can make is that the runtime is $O(n)$.
    > In casual conversation, programmers often neglect these formal differences,
    > but it is important to emphasize these formal differences when solving problems in this class or in an interview situation.

    The binary search algorithm greatly improved on sequential search by reducing the worst case runtime to $\Theta(\log n)$.

    > **NOTE:**
    > People often say informally that the binary search runtime is $O(\log n)$.
    > While that is a true statement, it is also a true statement that the binary search runtime is $O(n)$.
    > (Because $O$ is an upper bound and any large upper bound is guaranteed to also hold.)
    > Because the big-O notation can potentially be loose in this way and mask the improvement of binary search over sequential search,
    > we prefer to be excplicit with $\Theta$ when possible.

    But is $\Theta(\log n)$ the best we can do?
    If splitting the data into 2 recursive subproblems was good,
    maybe splitting it into 3 recursive subproblems will be better.
    The `trinary_search` function does just that.

    Your task is to analyze the runtime of this function.

    1. First we will analyze the runtime theoretically.
        Modify the README file to include:
    
        1. The recurrence relation that describes the function's runtime:
            $$T(n) = T(n/3) + 1$$

        1. The solution to the recurrence you wrote above as provided by the master theorem:
            $$T(n) = \Theta(log n)$$

        (Feel free to check your answers with me before moving on.)
    
    1. Next, we will use the timeit module to analyze the function empirically.
        The theoretical results above should give you a good prediction about how the empirical experiments below will turn out.

        Your task is to complete below that shows the actual runtime of the `binary_search` and `trinary_search` functions.
        To complete this table, modify the `timeit` command from the [Runtime vs N section of lab-timeit2](https://github.com/mikeizbicki/lab-timeit2#runtime-vs-n) so that it: (1) uses the appropriate functions from this lab, and (2) uses the numpy array instead of a list as the input data structure.
        As in the previous lab, I recommend using a bash for loop to complete this task.

        |                | `binary_search`           | `trinary_search`      |
        | -------------- | ------------------------- | --------------------- | 
        | `n=2**0`       |     0.802 usec            |       1.79 usec                |
        | `n=2**1`       |     1.55 usec                      |   3.26 usec                   |
        | `n=2**2`       |     2.24 usec                      |   3.44 usec                     |
        | `n=2**3`       |     2.63 usec                      |   3.15 usec                     |
        | `n=2**4`       |     3.17 usec                      |   0.581 usec                     |
        | `n=2**5`       |     3.68 usec                      |   3.19 usec                     |
        | `n=2**6`       |     4.29 usec                      |   6.93 usec                     |
        | `n=2**7`       |     4.76 usec                      |   6.14 usec                     |
        | `n=2**8`       |     5.36 usec                      |   8.1 usec                     |
        | `n=2**9`       |     5.72 usec                      |   5.06 usec                     |
        | `n=2**10`      |     6.51 usec                      |   7.54 usec                     |
        | `n=2**11`      |     6.95 usec                      |   9.22 usec                     |
        | `n=2**12`      |     7.12 usec                      |   9.54 usec                     |
        | `n=2**13`      |     7.55 usec                      |   9.8 usec                     |
        | `n=2**14`      |     8.1 usec                      |    12.8 usec                    |
        | `n=2**15`      |     8.55 usec                      |    12.9 usec                    |
        | `n=2**16`      |     9.13 usec                      |    14.1 usec                    |
        | `n=2**17`      |     10.1 usec                      |    13.5 usec                    |
        | `n=2**18`      |     10.9 usec                      |    15.5 usec                    |
        | `n=2**19`      |     11.5 usec                      |    13.1 usec                    |
        | `n=2**20`      |     12.5 usec                      |    18 usec                    |
        | `n=2**21`      |     13.9 usec                      |    18.9 usec                    |
        | `n=2**22`      |     12.8 usec                      |    20.8 usec                    |


1. Use the master theorem to solve the following recurrence relations,
    and modify the table to include the solutions.
    There is no experimental portion for this problem.

    | recurrence           | solution                       | practical application                     |
    | -------------------- | ------------------------------ | ----------------------------------------- |
    | T(n) = T(n/2) + n    | $\Theta(                    )$ | runtime of the bad binary search          |
    | T(n) = T(n/2) + 1    | $\Theta(                    )$ | runtime of the correct binary search      |
    | T(n) = T(n/3) + 1    | $\Theta(                    )$ | runtime of "trinary search"               |
    | T(n) = 2T(n/2) + 1   | $\Theta(                    )$ | runtime for [finding the median of an unsorted list](https://en.wikipedia.org/wiki/Quickselect) |
    | T(n) = 2T(n/2) + n   | $\Theta(                    )$ | runtime of merge sort                     |
    | T(n) = 3T(n/3) + n   | $\Theta(                    )$ | runtime of a trinary merge sort           |
    | T(n) = T(n/2) + n^2  | $\Theta(                    )$ |                                           |
    | T(n) = 2T(n/2) + n^2 | $\Theta(                    )$ |                                           |
    | T(n) = 3T(n/2) + n^2 | $\Theta(                    )$ |                                           |
    | T(n) = 3T(n/2) + n   | $\Theta(                    )$ | runtime of [Karatsuba's integer multiplication algorithm](https://en.wikipedia.org/wiki/Karatsuba_algorithm); HINT: Case 1 |
    | T(n) = 7T(n/2) + n^2 | $\Theta(                    )$ | runtime of [Strassen's matrix multiplication algorithm](https://en.wikipedia.org/wiki/Strassen_algorithm) |

1. Upload your changes to github (and not gitlab) by using the following steps.

    1. Create a new github repo.
        Ensure that you do not add any default files/branches to this repo, and that it is created empty.

    1. Add this newly created github repo as a remote by running
        ```
        $ git remote add github $url
        ```
        where `$url` is the url of your new repo.

    1. Add and commit your changes like normal.
        Then run
        ```
        $ git push github master
        ```
    
    Notice that there is no problem working with both github and gitlab on a single repository.
    Major open source projects regularly are hosted on many providers ar the same time.
    For example, the linux kernel is [mirrored on gitlab here](https://gitlab.com/linux-kernel/linux) and on [github here](https://github.com/torvalds/linux),
    but they don't actually use either website as their primary development platform.
    Instead, this is handled by a custom web frontend at <https://kernel.org>.

## Submission

Upload the url of your github repo to sakai.
