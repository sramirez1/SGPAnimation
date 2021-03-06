SGPanimation
================

Purpose
-------

Purpose of this book is to develop an animation that takes advantage of **gganimate**, **tweenr**, and other R packages. The animations will hopefully provide an intuitive animation for how student growth percentiles are calculated using an approach *similar* to the NYC Department of Education.

**Disclaimer**: I contributed to this book in my own personal capacity. The views and content expressed here are my own and do not necessarily represent the views of the NYC Department of Education.

Student Growth
--------------

The NYC Department of Education (NYCDOE) calculates a student's growth over the course of an academic year by calculating a student growth percentile -- or an SGP. An SGP is a simple calculation where a student's achievement at the end of a year is compared to the achievement of other 'similar' students. Typically, similar students -- commonly referred to as *peer* students -- are defined as students that start the school year with similar prior achievement scores. The NYCDOE defines peer students differently. Instead of defining peer students based only on their prior achievement scores at the start of the school year, the NYCDOE clusters similar students based on prior achievement scores *and* demographic characteristic (e.g. English language learner status, student with disability status, etc.).

To cluster similar students, the NYCDOE estimates what a student will score at the end of a year by running a **regression**. That's just a fancy of way of saying they use all the prior achievement scores and demographic characteristics they have to make an educated guess on what a student *should* score at the end of the year. \[*add footnote explaining that NYCDOE uses demographics as well*\]

Let's walk through a series of animations to get a better understanding of how the NYCDOE estimates a students EOY score and how that estimate is used to group similar students.

Students of All Backgrounds
---------------------------

Imagine we're trying to identify similar students from a very large pool of students represented by the points in space below. Each point represents a single student with a combination of incoming prior achievement score, demographic characteristics, and actual EOY score represented by varying size and color. We want to use the relationship between prior achievement, demographics, and actual EOY score to predict a student's EOY score.

![appear](SGPAnimationFiles/fig-appear-.gif)

Plot the Students
-----------------

Visualizing a regression over all these parameters -- prior achievement and demographics -- would be difficult as it would be over a multi-dimensional space. To simplify the visualization, let's focus our attention on the relationship between actual EOY score and prior achievement and assume that the regression is only run with prior achievement. Now, we can breakdown the points shown above and plot them on a 2D plane, with prior achievement on the horizontal-axis and EOY achievement on the vertical-axis. The result is a more formal representation of the dizzying display shown above -- a scatterplot of points.

![plot](SGPAnimationFiles/fig-plot-.gif)

Fit a Regression Line
---------------------

Now we're in a position to formalize the relationship between prior achievement and EOY achievement via a **linear regression**. The underlying mechanics of a linear regression can be complex, but intuitively a linear regression is simply a way to find a line that best *fits* a scatterplot of points. And by best fit, we mean a line that minimizes the sum of the vertical distance between every point and the line. \[*Add footnote explaining the sum of squared error?*\]

![lm](SGPAnimationFiles/fig-lm-.gif)

Estimate Fitted EOY Achievement
-------------------------------

Once the linear regression has settled on a line, we can move forward and estimate what we think each student should score on the EOY assessment based on their prior achievement score. Using the regression line, we can identify a corresponding EOY score for every prior achievement score. In effect, we estimate that every student will fall somewhere on the regression line depending on their prior achievement score. Of course, we know the *actual* EOY achievement score for every student, so why are we estimating what we *think* the EOY score will be? The reason is that, at this point, we are still trying to identify groups of similar students. Our estimate for each student's EOY score is the criteria we use to identify groups of similar students.

![predict](SGPAnimationFiles/fig-predict-.gif)

Assign peer groups for each student
-----------------------------------

Each student is assigned a group of similar students, or a peer group. The peer group is defined as the 50 nearest scores below a particular students EOY score and the 50 students nearest scores above a particular students EOY score. In the example below, the green point represents our reference student, or the student for whom we are creating a peer group. The purple points on either side of the reference student are that student's peer group. This process is repeated for every student, so that every student will have a unique peer group.

![findPeers](SGPAnimationFiles/fig-findPeers-.gif)

Assign Student Growth Percentile
--------------------------------

Once we have selected the peer group for a student, we then rank the peer group and reference student by their **actual** EOY score. The resulting rank of the reference student compared to the peer group becomes that student's SGP, with a possible range of 1 to 100. For instance, if the actual EOY score of the reference student were higher than 92% of the students in her/his group, then the student’s SGP would be 92.

![assign](SGPAnimationFiles/fig-assign-.gif)

The above explanation is a simplified version of the SGP calculation performed by the NYCDOE. As noted earlier, the NYCDOE does not cluster students based on prior achievement data only, but also considers demographic characteristics. All simplifications were made to illustrate the calculation at a general level. For those interested in the detailed methodology used by the NYCDOE, the official technical report can be found [here](http://www.google.com)
