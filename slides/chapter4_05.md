---
type: slides
---

# Exploratory data analysis with tidy data

Notes: You just created a tidy version of this survey data, which allows you to quickly ask and answer many different kinds of questions in exploratory data analysis.

---

# Counting agreement

```r
tidy_sisters %>%
    count(value)
```

```out
# A tibble: 5 x 2
  value       n
  <int>   <int>
1     1 1303555
2     2  844311
3     3  645401
4     4 1108859
5     5 1110154
```

Notes: You can easily see how many times survey respondents chose each option on the agreement scale with just one call to dplyr's [`count()`](https://dplyr.tidyverse.org/reference/tally.html) function.

We can see here that 1 was the most commonly chosen option; this corresponds to "disagree very much". The options for disagree very much, agree very much, and agree somewhat are chosen much more often than the other two.

---

# Overall agreement with age

```r
tidy_sisters %>%
    group_by(age) %>%
    summarise(value = mean(value))
```

```out
# A tibble: 9 x 2
    age value
  <dbl> <dbl>
1  20.0  2.86
2  30.0  2.81
3  40.0  2.83
4  50.0  2.94
5  60.0  3.10
6  70.0  3.26
7  80.0  3.42
8  90.0  3.51
9 100    3.60
```

Notes: You can also check out how the overall answers to all survey questions vary with age. There were more statements on the survey that older respondents agreed with than statements younger respondents agreed with.

---

# Agreement on questions by age

```r
tidy_sisters %>%
    filter(key %in% paste0("v", 153:170)) %>%
    group_by(key, value) %>%
    summarise(age = mean(age)) %>%
    ggplot(aes(value, age, color = key)) +
    geom_line(alpha = 0.5, size = 1.5) +
    geom_point(size = 2) +
    facet_wrap(~key)
```

Notes: We can go a few steps further and dig into how the answers to individual questions depend on age. This code first filters to a subset of questions on the survey, groups by these survey questions and the possible answers to them, and then calculates the mean age for each possible answer to each of the questions we're considering. 

This is now getting closer to what we really care about and we can then pipe it to ggplot2 to make an exploratory plot to visualize these relationships. 📊

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/plots-for-ml-case-studies.001.png?raw=true)

Notes: This plot shows that subset of the questions on the survey. Let's talk through a few of them. 

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/plots-for-ml-case-studies.002.png?raw=true)

Notes: The first question in this plot, `v153`, slopes downward. This means that the more a respondent agreed with this statement, the younger she was. What was `v153` on the survey?

---

# Freedom of speech

"People who don't believe in God have as much right to freedom of speech as anyone else."

Notes: This item was a statement about support of freedom of speech, regardless of religious belief.

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/plots-for-ml-case-studies.003.png?raw=true)

Notes: Other panels of this plot look different. `v161`, for example, slopes upward, which means that the more a respondent agreed with this statement, the older she was. What was this statement?

---

# Conservatism and heritage

"I like conservatism because it represents a stand to preserve our glorious heritage."

Notes: This item on the survey was a statement about identifying with conservatism and heritage.

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/plots-for-ml-case-studies.004.png?raw=true)

Notes: Notice that some panels in the plot don't slope up or down; there is no strong trend with age for some statements. Let's look at `v165`; see how it is flat and we don't see any trends up or down.

---

# Vietnam War

"Catholics as a group should consider active opposition to US participation in Vietnam."

Notes: This statement was about the Vietnam War, which was in a pivotal period in 1967. There is no trend with age that we can see in this plot, meaning that we don't see evidence here that younger or older Catholic nuns had different opinions about the United States involvement in the war.

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/plots-for-ml-case-studies.001.png?raw=true)

Notes: These are the relationships that we want to build a machine learning model to understand and use for prediction. Exploratory data analysis is an important first step so that you as a machine learning practitioner understand something about your data and what your model will be capable of learning. 

Once you have done that important exploration, you can build a very simple model and then create training and testing sets. 💫

---

![Alt text](https://github.com/juliasilge/caret-ML-course/blob/master/img/validation.png?raw=true)

Notes: In this case study, you are going to split the original data into three sets:

- training, 
- validation, and 
- test sets. 

You've already used training and test sets throughout this course, and in this last case study we're going to talk about how to use a **validation set** to choose a model. 🧐

---

# Let's explore!

Notes: Now it's your turn to take your tidy dataset and practice exploring for yourself.








