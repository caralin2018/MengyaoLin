---
title: "Interaction terms in logit and probit model"
author: "Mengyao Lin"
date: '2019-04-29'
slug: interaction
tags: Interpretation
categories: Regression
---

Short summary:

1)	As I know, there is not a generally accepted idea about the relation between the main effect and the effect of interaction terms. And most statisticians do not recommend that analysist directly interpret the main effect through the interaction terms. 

2)	The null hypothesis of β<sub>3</sub> (the coefficients of the interaction term) is there is no interaction effect. If the p-value is less than 0.05, we could reject the null hypothesis, say that there's an interaction effect.

3)	Fortunately, we could do one right thing--calculate the coefficients. For more information, see [Logistic Regression: Interaction Terms](http://www.cantab.net/users/filimon/cursoFCDEF/will/logistic_interact.pdf) .

4)	Also, we could follow advice from Green (2010). Please see page 295-296 for more information. 

5)	Effective code is `inteff` (Norton,  Wang & Ai, 2004) in Stata. Please note that this command is sensitive to the place of variables.  

6) Figures are useful for interpretation. You could learn this from Improving Tests of Theories Positing Interaction (Berry, Golder, & Milton, 2012).

7) Please see Chapter 2 Section 3 in “Interaction effects in multiple regression” (Jaccard & Turrisi, 2003) for more information about the significance tests of interaction terms between a categorical variable and a continuous variable.

---------------------------------------------------------------------------

In fact, this is a discussion rather than a correct answer. You could see some links relate to this topic and find disagreement. For example, link #1:[Interpreting Interactions when Main Effects are Not Significant] (https://www.theanalysisfactor.com/interactions-main-effects-not-significant/), link #2 [Actually, You can Interpret Some Main Effects in the Presence of an Interaction] (https://www.theanalysisfactor.com/interpret-main-effects-interaction/), and link #3 [How to Interpret Main Effects When the Interaction Effect is not Significant] (https://stats.stackexchange.com/questions/31027/how-to-interpret-main-effects-when-the-interaction-effect-is-not-significant). 

The first person who conducted an in-depth discussion about this topic should be Chunrong Ai and Edward C. Norton (2003). They published a paper entitled “Interaction terms in logit and probit models” on Economics Letters. This journal is not included in the SSCI list, but it is indeed a decent journal. I believe what they said in their paper 

> "The interaction effect, which is often the variable of interest in applied econometrics, cannot be evaluated simply by looking at the sign, magnitude, or statistical significance of the coefficient on the interaction term when the model is nonlinear. Instead, the interaction effect requires computing the cross derivative or cross difference. "

Green (2010) had afterwards disagreements about Ai's paper. The focus of their argument is how to understand the partial effects of interaction terms. Green believes that statistical testing produces "uninformative" and "misleading" results. The reason why I am in favour of him is that the effect of interaction terms (i.e. X1* X2) is conditional on X1 and X2 (separate variables). This is complicated and dangerous for every analyst.

Finally, I have to mention my perception of research. In general, an equation is based on a theory, then we collect data and analyze it for verifying the consistency of theory and reality (Brue & Grant, 2013; Jaccard & Turrisi, 2003). 

Then the codes below are probably useful. X1 and X2 are independent variables, Y1 is dependent variable.

```Stata
*	Generate an interaction term 
generate inter = X1 * X2
*	Probit regression
probit $y Y1 X1 X2 inter $x
*	Compute interaction effects and standard errors in the probit model above
inteff $y Y1 X1 X2 inter $x
```

References:

Ai, C., & Norton, E. C. (2003). Interaction terms in logit and probit models. Economics Letters,80(1), 123-129. doi:10.1016/s0165-1765(03)00032-6

Berry, W. D., Golder, M., & Milton, D. (2012). Improving Tests of Theories Positing Interaction. The Journal of Politics,74(3), 653-671. doi:10.1017/s0022381612000199

Greene, W. (2010). Testing hypotheses about interaction terms in nonlinear models. Economics Letters,107(2), 291-296. doi:10.1016/j.econlet.2010.02.014

Jaccard, J., & Turrisi, R. (2003). Interaction effects in multiple regression. Thousand Oaks: Sage.

Norton, E. C., Wang, H., & Ai, C. (2004). Computing interaction effects and standard errors in logit and probit models. The Stata Journal, 4(2), 154-167.


