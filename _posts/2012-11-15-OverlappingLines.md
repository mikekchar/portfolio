---
layout: default
title: Puzzle - Find the Overlapping lines
permalink: OverlappingLines
category: Puzzles
description: How do we find out if lines overlap.
summary: This is the first in a series of puzzle posts.  If you have two number lines with several line segments on them, how do you efficiently determine which line segments on the number lines overlap?
---
## Aaargghh! My brain isn't working!

Yesterday someone asked me to solve this puzzle.  It is interesting and
not particularly difficult to solve, but to my embarrasment I was not
able to give a good accounting of myself at the time.  In my defence, I
am particularly bad at thinking in public.  For whatever reason my
brain freezes and nothing emerges.  That was the case yesterday and
it occurred to me that this is a good opportunity for improvement.  I've
therefore decided to make puzzles of this sort a permanent fixture in
my blog. The solution is in Python.  Please excuse any naive coding
as I am not yet fluent in Python.

### The Problem

Imagine 2 number lines like this:

![Number Lines](../images/NumberLines.png "Two Numberlines")

We can draw line segments along the number lines like this:

![Line Segments](../images/LineSegments.png "Line Segments")

In this example, the red line has 4 segments while the blue
line has 3 segments.  We can represent the segments by list
of tuples indicating the begining and ending coordinates of the
segment.  The red line is made up of the tuples:

    r = [(1,3), (6,10), (12,13), (17,20)]

While the blue line is made up of the tuples:

    b = [(2,4), (11,15), (18, 20)]


We want to find the segments that overlap.  In this case, red's first
tuple overlaps with blue's first tuple, red's third tuple overlaps
with blue's second tuple, and red's fouth tuple overlaps with blue's
third tuple.  We'll count from zero so we want the output to look like
this.

    [(0,0), (2,1), (3,2)]

Find a solution for the problem and state the O() complexity.

### The Solution

First let's write a function for determining if two segments overlap.
The easiest way to do this is actually to determine *where* they overlap.

    def overlapping_segment(a, b):
        x = max(a[0], b[0])
        y = min(a[1], b[1])
        return x,y

The function returns the segment where the two segments overlap.  If x is
less than y, the two segments overlap.  Otherwise they dont.

Now that we have this function, how should we iterate through the
segments to determine which ones overlap?
I have to admit that I struggled trying to find a good solution for this
problem.  The naive approach is to simply loop over each of the segments
trying to find out which ones intersect.  However, if the red line has
N segments and the blue lines have M segments, the complexity of this
solution is O(NxM); hardly effecient.  Can we do better?

The trick to this problem is realizing that when we compare two segments,
the one with the smallest right hand coordinate can not overlap with
any other segments.  For example, look at the first two segments (1,3) and
(2,4). They overlap, but the red segment can *only* overlap this particular
blue segment because it stops in the middle of the blue segment.

In fact, we want to iterate over the segments, increasing our counter
if the right hand coordinate of the overlapping segment equals the
right hand coordingate of the original segment.

    def find_overlaps(r, b):
        retVal = []
        ri = 0
        bi = 0
        while (ri < len(r)) or (bi < len(b)): 
            s = overlapping_segment(r[ri], b[bi])
            if s[0] < s[1]:
                retVal.append([ri, bi])
            if r[ri][1] == s[1]:
                ri = ri + 1
            if b[bi][1] == s[1]:
                bi = bi + 1
        return retVal

Since we are iterating over the each segment in each line exactly once,
the complexity of this solution is O(N+M) where N is the number
of segments in the red line and M is the number of segments in the
the blue line.

We can generalize this solution for many lines.  Instead of two lines,
red and blue, we have any number of lines.  Essentially we have a matrix
of lines segments.

    def find_multiple_overlaps(m):
        retVal = []
        # We have a vector of indeces.  One for each line.
        indeces = [0] * len(m)
        sizes = [len(line) for line in m]
        while indeces < sizes:
            # Slice the matrix to get a list of line segments
            # associated with the indeces.
            segments = [m[i][index] for i,index in enumerate(indeces)]
            s = max([x for x,y in segments]), min([y for x,y in segments])
            if s[0] < s[1]:
                retVal.append(tuple(indeces))

            # Increment the approriate indeces.
            for i,segment in enumerate(segments):
                if segment[1] == s[1]:
                    indeces[i] = indeces[i] + 1
        return retVal

