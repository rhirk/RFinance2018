-   [Example 1 - A simple example with 2
    raters](#example-1---a-simple-example-with-2-raters)
-   [Example 2 - A simple example with 2
    raters](#example-2---a-simple-example-with-2-raters)
-   [Example 3a - A model of firm ratings assigned by multiple raters
    and IG-SG
    indicator](#example-3a---a-model-of-firm-ratings-assigned-by-multiple-raters-and-ig-sg-indicator)
-   [Example 3b - A more elaborate model of ratings assigned by multiple
    raters](#example-3b---a-more-elaborate-model-of-ratings-assigned-by-multiple-raters)
-   [Example 4 - A longitudinal
    model](#example-4---a-longitudinal-model)

Further more details on the package **mvord** see
<https://cran.r-project.org/web/packages/mvord/vignettes/vignette_mvord.pdf>.

Load package **mvord**

    library(mvord)

Load data set

    data("data_cr")
    str(data_cr, vec.len = 3)

    ## 'data.frame':    690 obs. of  10 variables:
    ##  $ rater1 : Ord.factor w/ 5 levels "A"<"B"<"C"<"D"<..: 2 3 3 2 5 4 3 4 ...
    ##  $ rater2 : Ord.factor w/ 5 levels "A"<"B"<"C"<"D"<..: 2 4 4 2 5 NA 3 4 ...
    ##  $ rater3 : Ord.factor w/ 6 levels "F"<"G"<"H"<"I"<..: 3 NA NA NA 6 NA 2 5 ...
    ##  $ rater4 : Ord.factor w/ 2 levels "L"<"M": 1 2 2 1 2 2 2 2 ...
    ##  $ firm_id: int  1 2 3 4 5 6 7 8 ...
    ##  $ LR     : num  1.72 1.84 2.64 1.31 ...
    ##  $ LEV    : num  2.114 0.883 2.3 2.638 ...
    ##  $ PR     : num  0.3779 -0.1503 -0.0521 0.3289 ...
    ##  $ RSIZE  : num  -6.37 -7.84 -7.98 -5.86 ...
    ##  $ BETA   : num  0.836 0.49 0.802 1.137 ...

    head(data_cr, n = 3)

    ##   rater1 rater2 rater3 rater4 firm_id       LR       LEV          PR
    ## 1      B      B      H      L       1 1.720041 2.1144513  0.37792213
    ## 2      C      D   <NA>      M       2 1.836574 0.8826725 -0.15032402
    ## 3      C      D   <NA>      M       3 2.638177 2.2997237 -0.05205389
    ##       RSIZE      BETA
    ## 1 -6.365053 0.8358773
    ## 2 -7.839813 0.4895358
    ## 3 -7.976650 0.8022900

Example 1 - A simple example with 2 raters
------------------------------------------

A simple example with 2 raters (rater1 and rater2). The data set
data\_cr has a wide format and hence, we apply the multiple measurement
object MMO2 on the left-hand side of the formula object. The covariates
LR, LEV, PR, RSIZE, BETA are passed on the right-hand side of the
formula. The thresholds are set equal by the argument
thresholds.constraints.

    res_cor_probit_2raters <- mvord(formula = MMO2(rater1, rater2) ~ 0 + LR + LEV + PR + RSIZE + BETA,
                                   threshold.constraints = c(1, 1),
                                   data = data_cr)

The results are displayed by:

    summary(res_cor_probit_2raters)

    ## 
    ## Call: mvord(formula = MMO2(rater1, rater2) ~ 0 + LR + LEV + PR + RSIZE + 
    ##     BETA, data = data_cr, threshold.constraints = c(1, 1))
    ## 
    ## Formula: MMO2(rater1, rater2) ~ 0 + LR + LEV + PR + RSIZE + BETA
    ## 
    ##     link threshold nsubjects ndim   logPL   CLAIC   CLBIC fevals
    ## mvprobit  flexible       690    2 -799.84 1630.35 1699.91   3218
    ## 
    ## Thresholds:
    ##            Estimate Std. Error z value  Pr(>|z|)    
    ## rater1 A|B  8.40534    0.39600  21.225 < 2.2e-16 ***
    ## rater1 B|C  9.87575    0.42661  23.149 < 2.2e-16 ***
    ## rater1 C|D 11.68479    0.46471  25.145 < 2.2e-16 ***
    ## rater1 D|E 14.00772    0.53773  26.050 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Coefficients:
    ##          Estimate Std. Error  z value  Pr(>|z|)    
    ## LR 1     0.191815   0.059864   3.2042  0.001354 ** 
    ## LR 2     0.089980   0.069426   1.2961  0.194953    
    ## LEV 1    0.456827   0.039714  11.5028 < 2.2e-16 ***
    ## LEV 2    0.441118   0.044323   9.9523 < 2.2e-16 ***
    ## PR 1    -2.626682   0.174938 -15.0149 < 2.2e-16 ***
    ## PR 2    -2.761411   0.203692 -13.5568 < 2.2e-16 ***
    ## RSIZE 1 -1.166861   0.050982 -22.8878 < 2.2e-16 ***
    ## RSIZE 2 -1.184522   0.050259 -23.5685 < 2.2e-16 ***
    ## BETA 1   1.644008   0.100520  16.3550 < 2.2e-16 ***
    ## BETA 2   1.741845   0.128535  13.5515 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Error Structure:
    ##                    Estimate Std. Error z value  Pr(>|z|)    
    ## corr rater1 rater2 0.872025   0.025461   34.25 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The coefficients can be extracted by:

    coef(res_cor_probit_2raters)

    ##        LR 1        LR 2       LEV 1       LEV 2        PR 1        PR 2 
    ##  0.19181519  0.08998022  0.45682662  0.44111809 -2.62668211 -2.76141092 
    ##     RSIZE 1     RSIZE 2      BETA 1      BETA 2 
    ## -1.16686094 -1.18452182  1.64400769  1.74184465

Example 2 - A simple example with 2 raters
------------------------------------------

A simple example with 3 raters (rater1, rater2 and rater3). The
regression coefficients are set equal by the argument coef.constraints.

    res_cor_probit_3raters <- mvord(formula = MMO2(rater1, rater2, rater 3) ~ 0 + LR + LEV + PR + RSIZE + BETA,
                                   coef.constraints = c(1, 1, 1),
                                   data = data_cr,
                                   link = mvlogit())

The results are displayed by:

    summary(res_cor_probit_3raters)

    ## 
    ## Call: mvord(formula = MMO2(rater1, rater2, rater3) ~ 0 + LR + LEV + 
    ##     PR + RSIZE + BETA, data = data_cr, link = mvlogit(), coef.constraints = c(1, 
    ##     1, 1))
    ## 
    ## Formula: MMO2(rater1, rater2, rater3) ~ 0 + LR + LEV + PR + RSIZE + BETA
    ## 
    ##    link threshold nsubjects ndim   logPL   CLAIC   CLBIC fevals
    ## mvlogit  flexible       690    3 -1561.4 3194.64 3357.58   4222
    ## 
    ## Thresholds:
    ##            Estimate Std. Error z value  Pr(>|z|)    
    ## rater1 A|B 14.71273    0.84962  17.317 < 2.2e-16 ***
    ## rater1 B|C 17.46132    0.92699  18.837 < 2.2e-16 ***
    ## rater1 C|D 20.65829    1.03917  19.880 < 2.2e-16 ***
    ## rater1 D|E 24.68645    1.20698  20.453 < 2.2e-16 ***
    ## rater2 A|B 14.87020    0.85299  17.433 < 2.2e-16 ***
    ## rater2 B|C 17.43897    0.93096  18.732 < 2.2e-16 ***
    ## rater2 C|D 20.47189    1.04358  19.617 < 2.2e-16 ***
    ## rater2 D|E 24.80045    1.22174  20.299 < 2.2e-16 ***
    ## rater3 F|G 14.66330    0.86375  16.976 < 2.2e-16 ***
    ## rater3 G|H 17.35099    0.92572  18.743 < 2.2e-16 ***
    ## rater3 H|I 20.73809    1.04700  19.807 < 2.2e-16 ***
    ## rater3 I|J 23.25685    1.15044  20.216 < 2.2e-16 ***
    ## rater3 J|K 25.33849    1.22854  20.625 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Coefficients:
    ##          Estimate Std. Error  z value  Pr(>|z|)    
    ## LR 1     0.333598   0.112624   2.9621  0.003056 ** 
    ## LEV 1    0.746847   0.076165   9.8057 < 2.2e-16 ***
    ## PR 1    -4.930267   0.356519 -13.8289 < 2.2e-16 ***
    ## RSIZE 1 -2.073425   0.108014 -19.1958 < 2.2e-16 ***
    ## BETA 1   3.021152   0.222735  13.5639 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Error Structure:
    ##                    Estimate Std. Error z value  Pr(>|z|)    
    ## corr rater1 rater2 0.866603   0.027446  31.575 < 2.2e-16 ***
    ## corr rater1 rater3 0.903774   0.024724  36.554 < 2.2e-16 ***
    ## corr rater2 rater3 0.822653   0.045875  17.933 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The threshold parameters are presented by:

    thresholds(res_cor_probit_3raters)

    ## $rater1
    ##      A|B      B|C      C|D      D|E 
    ## 14.71273 17.46132 20.65829 24.68645 
    ## 
    ## $rater2
    ##      A|B      B|C      C|D      D|E 
    ## 14.87020 17.43897 20.47189 24.80045 
    ## 
    ## $rater3
    ##      F|G      G|H      H|I      I|J      J|K 
    ## 14.66330 17.35099 20.73809 23.25685 25.33849

Example 3a - A model of firm ratings assigned by multiple raters and IG-SG indicator
------------------------------------------------------------------------------------

This example presents a multivariate ordinal regression model with
probit link and a general correlation error structure (cor\_general(~
1)).

    res_cor_probit_simple <- mvord(formula = MMO2(rater1, rater2, rater3,
      rater4) ~ 0 + LR + LEV + PR + RSIZE + BETA, data = data_cr)

The results are displayed by:

    summary(res_cor_probit_simple)

    ## 
    ## Call: mvord(formula = MMO2(rater1, rater2, rater3, rater4) ~ 0 + LR + 
    ##     LEV + PR + RSIZE + BETA, data = data_cr)
    ## 
    ## Formula: MMO2(rater1, rater2, rater3, rater4) ~ 0 + LR + LEV + PR + RSIZE + 
    ##     BETA
    ## 
    ##     link threshold nsubjects ndim    logPL   CLAIC   CLBIC fevals
    ## mvprobit  flexible       690    4 -2925.79 6037.29 6458.57   6139
    ## 
    ## Thresholds:
    ##            Estimate Std. Error z value  Pr(>|z|)    
    ## rater1 A|B  8.05308    0.44312  18.174 < 2.2e-16 ***
    ## rater1 B|C  9.57196    0.47384  20.201 < 2.2e-16 ***
    ## rater1 C|D 11.35469    0.51753  21.940 < 2.2e-16 ***
    ## rater1 D|E 13.52181    0.60134  22.486 < 2.2e-16 ***
    ## rater2 A|B  8.59974    0.49820  17.262 < 2.2e-16 ***
    ## rater2 B|C 10.06007    0.53930  18.654 < 2.2e-16 ***
    ## rater2 C|D 11.86508    0.59726  19.866 < 2.2e-16 ***
    ## rater2 D|E 14.34057    0.70069  20.466 < 2.2e-16 ***
    ## rater3 F|G  8.24546    0.51708  15.946 < 2.2e-16 ***
    ## rater3 G|H  9.77754    0.55527  17.608 < 2.2e-16 ***
    ## rater3 H|I 11.70957    0.62261  18.807 < 2.2e-16 ***
    ## rater3 I|J 13.09715    0.68735  19.055 < 2.2e-16 ***
    ## rater3 J|K 14.17708    0.72080  19.669 < 2.2e-16 ***
    ## rater4 L|M 13.54304    1.00738  13.444 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Coefficients:
    ##          Estimate Std. Error  z value  Pr(>|z|)    
    ## LR 1     0.208387   0.067996   3.0647  0.002179 ** 
    ## LR 2     0.153527   0.073349   2.0931  0.036340 *  
    ## LR 3     0.180650   0.078391   2.3045  0.021195 *  
    ## LR 4     0.150135   0.112011   1.3404  0.180128    
    ## LEV 1    0.430524   0.043758   9.8388 < 2.2e-16 ***
    ## LEV 2    0.433143   0.050132   8.6400 < 2.2e-16 ***
    ## LEV 3    0.399637   0.050768   7.8719 3.493e-15 ***
    ## LEV 4    0.626346   0.074278   8.4325 < 2.2e-16 ***
    ## PR 1    -2.574577   0.194047 -13.2678 < 2.2e-16 ***
    ## PR 2    -2.829004   0.216932 -13.0410 < 2.2e-16 ***
    ## PR 3    -2.679726   0.222574 -12.0397 < 2.2e-16 ***
    ## PR 4    -2.797267   0.281530  -9.9360 < 2.2e-16 ***
    ## RSIZE 1 -1.130529   0.056380 -20.0518 < 2.2e-16 ***
    ## RSIZE 2 -1.197017   0.061751 -19.3845 < 2.2e-16 ***
    ## RSIZE 3 -1.196935   0.066398 -18.0266 < 2.2e-16 ***
    ## RSIZE 4 -1.567831   0.116397 -13.4696 < 2.2e-16 ***
    ## BETA 1   1.602576   0.110842  14.4581 < 2.2e-16 ***
    ## BETA 2   1.802612   0.140077  12.8687 < 2.2e-16 ***
    ## BETA 3   1.517178   0.139209  10.8985 < 2.2e-16 ***
    ## BETA 4   1.990449   0.204850   9.7166 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Error Structure:
    ##                    Estimate Std. Error z value  Pr(>|z|)    
    ## corr rater1 rater2 0.874183   0.024864  35.158 < 2.2e-16 ***
    ## corr rater1 rater3 0.914814   0.023171  39.481 < 2.2e-16 ***
    ## corr rater1 rater4 0.900697   0.031939  28.201 < 2.2e-16 ***
    ## corr rater2 rater3 0.837847   0.041416  20.230 < 2.2e-16 ***
    ## corr rater2 rater4 0.926213   0.031728  29.192 < 2.2e-16 ***
    ## corr rater3 rater4 0.845626   0.060134  14.062 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The threshold coefficients can be extracted by:

    thresholds(res_cor_probit_simple)

    ## $rater1
    ##       A|B       B|C       C|D       D|E 
    ##  8.053083  9.571962 11.354686 13.521806 
    ## 
    ## $rater2
    ##       A|B       B|C       C|D       D|E 
    ##  8.599739 10.060068 11.865083 14.340568 
    ## 
    ## $rater3
    ##       F|G       G|H       H|I       I|J       J|K 
    ##  8.245461  9.777541 11.709568 13.097152 14.177082 
    ## 
    ## $rater4
    ##      L|M 
    ## 13.54304

The regression coefficients are obtained by:

    coef(res_cor_probit_simple)

    ##       LR 1       LR 2       LR 3       LR 4      LEV 1      LEV 2 
    ##  0.2083869  0.1535266  0.1806502  0.1501350  0.4305235  0.4331427 
    ##      LEV 3      LEV 4       PR 1       PR 2       PR 3       PR 4 
    ##  0.3996369  0.6263461 -2.5745773 -2.8290041 -2.6797255 -2.7972672 
    ##    RSIZE 1    RSIZE 2    RSIZE 3    RSIZE 4     BETA 1     BETA 2 
    ## -1.1305294 -1.1970173 -1.1969355 -1.5678310  1.6025757  1.8026120 
    ##     BETA 3     BETA 4 
    ##  1.5171782  1.9904487

The error structure for firm with firm\_id = 11 is displayed by:

    error_structure(res_cor_probit_simple)[[11]]

    ##           rater1    rater2    rater3    rater4
    ## rater1 1.0000000 0.8741830 0.9148139 0.9006967
    ## rater2 0.8741830 1.0000000 0.8378465 0.9262133
    ## rater3 0.9148139 0.8378465 1.0000000 0.8456261
    ## rater4 0.9006967 0.9262133 0.8456261 1.0000000

Example 3b - A more elaborate model of ratings assigned by multiple raters
--------------------------------------------------------------------------

In this example, we extend the setting of the above example by imposing
constraints on the regression as well as on the threshold parameters and
changing the link function to the multivariate logit link.

    res_cor_logit <- mvord(formula = MMO2(rater1, rater2, rater3, rater4) ~
        0 + LR + LEV + PR + RSIZE + BETA, data = data_cr, link = mvlogit(),
        coef.constraints = cbind(LR = c(1, 1, 1, 1), LEV = c(1, 2, 3, 4),
          PR = c(1, 1, 1, 1), RSIZE = c(1, 1, 1, 2), BETA = c(1, 1, 2, 3)),
        threshold.constraints = c(1, 1, 2, 3))

The results are displayed by:

    summary(res_cor_logit)

    ## 
    ## Call: mvord(formula = MMO2(rater1, rater2, rater3, rater4) ~ 0 + LR + 
    ##     LEV + PR + RSIZE + BETA, data = data_cr, link = mvlogit(), 
    ##     coef.constraints = cbind(c(1, 1, 1, 1), c(1, 2, 3, 4), c(1, 
    ##         1, 1, 1), c(1, 1, 1, 2), c(1, 1, 2, 3)), threshold.constraints = c(1, 
    ##         1, 2, 3))
    ## 
    ## Formula: MMO2(rater1, rater2, rater3, rater4) ~ 0 + LR + LEV + PR + RSIZE + 
    ##     BETA
    ## 
    ##    link threshold nsubjects ndim    logPL   CLAIC   CLBIC fevals
    ## mvlogit  flexible       690    4 -2926.42 5987.81 6293.98  10626
    ## 
    ## Thresholds:
    ##            Estimate Std. Error z value  Pr(>|z|)    
    ## rater1 A|B 15.04918    0.82409  18.262 < 2.2e-16 ***
    ## rater1 B|C 17.75219    0.89727  19.785 < 2.2e-16 ***
    ## rater1 C|D 20.97822    1.00773  20.817 < 2.2e-16 ***
    ## rater1 D|E 25.13048    1.17487  21.390 < 2.2e-16 ***
    ## rater3 F|G 14.47061    0.83922  17.243 < 2.2e-16 ***
    ## rater3 G|H 17.17327    0.89515  19.185 < 2.2e-16 ***
    ## rater3 H|I 20.56635    1.01119  20.339 < 2.2e-16 ***
    ## rater3 I|J 23.00524    1.11045  20.717 < 2.2e-16 ***
    ## rater3 J|K 24.97259    1.18725  21.034 < 2.2e-16 ***
    ## rater4 L|M 23.92769    1.63196  14.662 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Coefficients:
    ##          Estimate Std. Error  z value  Pr(>|z|)    
    ## LR 1     0.340210   0.110547   3.0775  0.002087 ** 
    ## LEV 1    0.784295   0.075977  10.3228 < 2.2e-16 ***
    ## LEV 2    0.779695   0.078364   9.9497 < 2.2e-16 ***
    ## LEV 3    0.718330   0.093425   7.6889 1.484e-14 ***
    ## LEV 4    1.107836   0.123681   8.9572 < 2.2e-16 ***
    ## PR 1    -4.917965   0.343464 -14.3187 < 2.2e-16 ***
    ## RSIZE 1 -2.093379   0.103690 -20.1889 < 2.2e-16 ***
    ## RSIZE 2 -2.746162   0.188731 -14.5507 < 2.2e-16 ***
    ## BETA 1   3.135693   0.221944  14.1283 < 2.2e-16 ***
    ## BETA 2   2.733086   0.252960  10.8044 < 2.2e-16 ***
    ## BETA 3   3.572688   0.349493  10.2225 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Error Structure:
    ##                    Estimate Std. Error z value  Pr(>|z|)    
    ## corr rater1 rater2 0.859773   0.027907  30.808 < 2.2e-16 ***
    ## corr rater1 rater3 0.908834   0.024636  36.891 < 2.2e-16 ***
    ## corr rater1 rater4 0.903959   0.031857  28.375 < 2.2e-16 ***
    ## corr rater2 rater3 0.834910   0.044258  18.865 < 2.2e-16 ***
    ## corr rater2 rater4 0.932243   0.032172  28.977 < 2.2e-16 ***
    ## corr rater3 rater4 0.856221   0.058398  14.662 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The constraints are displayed by:

    constraints(res_cor_logit)

    ## $LR
    ##     LR 1
    ## A|B    1
    ## B|C    1
    ## C|D    1
    ## D|E    1
    ## A|B    1
    ## B|C    1
    ## C|D    1
    ## D|E    1
    ## F|G    1
    ## G|H    1
    ## H|I    1
    ## I|J    1
    ## J|K    1
    ## L|M    1
    ## 
    ## $LEV
    ##     LEV 1 LEV 2 LEV 3 LEV 4
    ## A|B     1     0     0     0
    ## B|C     1     0     0     0
    ## C|D     1     0     0     0
    ## D|E     1     0     0     0
    ## A|B     0     1     0     0
    ## B|C     0     1     0     0
    ## C|D     0     1     0     0
    ## D|E     0     1     0     0
    ## F|G     0     0     1     0
    ## G|H     0     0     1     0
    ## H|I     0     0     1     0
    ## I|J     0     0     1     0
    ## J|K     0     0     1     0
    ## L|M     0     0     0     1
    ## 
    ## $PR
    ##     PR 1
    ## A|B    1
    ## B|C    1
    ## C|D    1
    ## D|E    1
    ## A|B    1
    ## B|C    1
    ## C|D    1
    ## D|E    1
    ## F|G    1
    ## G|H    1
    ## H|I    1
    ## I|J    1
    ## J|K    1
    ## L|M    1
    ## 
    ## $RSIZE
    ##     RSIZE 1 RSIZE 2
    ## A|B       1       0
    ## B|C       1       0
    ## C|D       1       0
    ## D|E       1       0
    ## A|B       1       0
    ## B|C       1       0
    ## C|D       1       0
    ## D|E       1       0
    ## F|G       1       0
    ## G|H       1       0
    ## H|I       1       0
    ## I|J       1       0
    ## J|K       1       0
    ## L|M       0       1
    ## 
    ## $BETA
    ##     BETA 1 BETA 2 BETA 3
    ## A|B      1      0      0
    ## B|C      1      0      0
    ## C|D      1      0      0
    ## D|E      1      0      0
    ## A|B      1      0      0
    ## B|C      1      0      0
    ## C|D      1      0      0
    ## D|E      1      0      0
    ## F|G      0      1      0
    ## G|H      0      1      0
    ## H|I      0      1      0
    ## I|J      0      1      0
    ## J|K      0      1      0
    ## L|M      0      0      1

Note that the composite likelihood information criteria can be used for
model comparison. For objects of class ‘mvord’ CLAIC and CLBIC are
computed by AIC() and BIC(), respectively. The model fits of examples
one and two are compared by means of BIC and AIC. We observe that the
model of Example 3b has a lower BIC and AIC indicating a better model
fit:

    BIC(res_cor_probit_simple)

    ## [1] 6458.566

    BIC(res_cor_logit)

    ## [1] 6293.977

    AIC(res_cor_probit_simple)

    ## [1] 6037.293

    AIC(res_cor_logit)

    ## [1] 5987.81

The value of the pairwise log-likelihood of the two models can be
extracted by:

    logLik(res_cor_probit_simple)

    ## 'log Lik.' -2925.788 (df=92.85905)

    logLik(res_cor_logit)

    ## 'log Lik.' -2926.418 (df=67.48687)

Marginal predictions are obtained by:

    mp <- marginal_predict(res_cor_logit, type = "class")

    table(res_cor_logit$rho$y[,1], mp[,1])

    ##    
    ##       A   B   C   D   E
    ##   A  47  23   4   0   0
    ##   B  11  65  44   3   0
    ##   C   0  28 135  38   0
    ##   D   1   2  44 116  17
    ##   E   0   0   0  30  47

    table(res_cor_logit$rho$y[,2], mp[,2])

    ##    
    ##       A   B   C   D   E
    ##   A  29  20   8   0   0
    ##   B  12  41  22   2   0
    ##   C   1  18 103  24   0
    ##   D   0   0  35 109   7
    ##   E   0   0   0  13  39

    table(res_cor_logit$rho$y[,3], mp[,3])

    ##    
    ##      F  G  H  I  J  K
    ##   F 25  8  2  0  0  0
    ##   G  4 33 23  1  0  0
    ##   H  1 18 85 13  0  0
    ##   I  0  0 28 30  3  2
    ##   J  0  0  2 13 10  7
    ##   K  0  0  0  6  8 23

    table(res_cor_logit$rho$y[,4], mp[,4])

    ##    
    ##       L   M
    ##   L 195  40
    ##   M  30 425

Joint predictions are obtained by:

    jp <- joint_probabilities(res_cor_logit, type = "class")

    table(res_cor_logit$rho$y[,1], jp[,1])

    ##    
    ##       A   B   C   D   E
    ##   A  50  20   4   0   0
    ##   B  11  68  41   3   0
    ##   C   0  36 130  35   0
    ##   D   1   2  47 112  18
    ##   E   0   0   0  25  52

    table(res_cor_logit$rho$y[,2], jp[,2])

    ##    
    ##       A   B   C   D   E
    ##   A  33  17   7   0   0
    ##   B  12  46  17   2   0
    ##   C   1  24  99  22   0
    ##   D   0   0  39 103   9
    ##   E   0   0   0  10  42

    table(res_cor_logit$rho$y[,3], jp[,3])

    ##    
    ##      F  G  H  I  J  K
    ##   F 27  7  1  0  0  0
    ##   G  6 33 21  1  0  0
    ##   H  1 24 77 15  0  0
    ##   I  0  0 25 35  1  2
    ##   J  0  0  2 17  3 10
    ##   K  0  0  0  9  1 27

    table(res_cor_logit$rho$y[,4], jp[,4])

    ##    
    ##       L   M
    ##   L 175  60
    ##   M  22 433

Example 4 - A longitudinal model
--------------------------------

In this example, we present a longitudinal multivariate ordinal probit
regression model with a covariate dependent AR(1) error structure using
the data set data\_cr\_panel:

    data(data_cr_panel)
    str(data_cr_panel, vec.len = 3)

    ## 'data.frame':    11320 obs. of  9 variables:
    ##  $ rating : Ord.factor w/ 5 levels "A"<"B"<"C"<"D"<..: 5 3 3 3 3 1 3 3 ...
    ##  $ firm_id: int  1 2 3 4 5 6 7 8 ...
    ##  $ year   : Factor w/ 8 levels "year1","year2",..: 1 1 1 1 1 1 1 1 ...
    ##  $ LR     : num  572.86 1.38 7.46 10.9 ...
    ##  $ LEV    : num  1.2008 0.0302 0.1517 0.5485 ...
    ##  $ PR     : num  0.1459 -0.0396 0.0508 0.1889 ...
    ##  $ RSIZE  : num  1.423 -1.944 2.024 -0.433 ...
    ##  $ BETA   : num  1.148 1.693 0.761 2.24 ...
    ##  $ BSEC   : Factor w/ 8 levels "BSEC1","BSEC2",..: 3 6 3 7 6 7 7 7 ...

    head(data_cr_panel, n = 3)

    ##   rating firm_id  year         LR        LEV          PR     RSIZE
    ## 1      E       1 year1 572.864658 1.20084294  0.14585117  1.422948
    ## 2      C       2 year1   1.379547 0.03022761 -0.03962597 -1.944265
    ## 3      C       3 year1   7.462706 0.15170420  0.05083517  2.024098
    ##        BETA  BSEC
    ## 1 1.1481020 BSEC3
    ## 2 1.6926956 BSEC6
    ## 3 0.7610057 BSEC3

    res_AR1_probit <- mvord(formula = MMO(rating, firm_id, year) ~ LR + LEV +
      PR + RSIZE + BETA, error.structure = cor_ar1(~ BSEC), link = mvprobit(),
      data = data_cr_panel, coef.constraints = c(rep(1, 4), rep(2, 4)),
      threshold.constraints = rep(1, 8), threshold.values = rep(list(c(0, NA,
        NA, NA)),8), mvord.control(solver = "BFGS"))

The results of the model can be presented by

    summary(res_AR1_probit, short = TRUE, call = FALSE)

    ## Formula: MMO(rating, firm_id, year) ~ LR + LEV + PR + RSIZE + BETA
    ## 
    ##     link threshold nsubjects ndim     logPL     CLAIC     CLBIC fevals
    ## mvprobit fix1first      1415    8 -77843.09 156104.49 157203.55    189
    ## 
    ## Thresholds:
    ##           Estimate Std. Error z value  Pr(>|z|)    
    ## year1 A|B 0.000000   0.000000      NA        NA    
    ## year1 B|C 0.984647   0.025802  38.162 < 2.2e-16 ***
    ## year1 C|D 2.364711   0.039873  59.306 < 2.2e-16 ***
    ## year1 D|E 3.728002   0.055724  66.901 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Coefficients:
    ##                  Estimate  Std. Error  z value  Pr(>|z|)    
    ## (Intercept) 1  1.42471225  0.04556961  31.2645 < 2.2e-16 ***
    ## (Intercept) 2  1.49164394  0.05786976  25.7759 < 2.2e-16 ***
    ## LR 1           0.02142909  0.00054203  39.5346 < 2.2e-16 ***
    ## LR 2           0.02959425  0.00096574  30.6442 < 2.2e-16 ***
    ## LEV 1          0.01114252  0.00052558  21.2004 < 2.2e-16 ***
    ## LEV 2          0.01390128  0.00081658  17.0238 < 2.2e-16 ***
    ## PR 1          -0.87154954  0.03320032 -26.2512 < 2.2e-16 ***
    ## PR 2          -0.67501624  0.04542960 -14.8585 < 2.2e-16 ***
    ## RSIZE 1       -0.34752657  0.00995679 -34.9035 < 2.2e-16 ***
    ## RSIZE 2       -0.35102290  0.01354452 -25.9162 < 2.2e-16 ***
    ## BETA 1         0.04802612  0.02197463   2.1855  0.028850 *  
    ## BETA 2         0.08627324  0.03090444   2.7916  0.005245 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Error Structure:
    ##              Estimate Std. Error  z value  Pr(>|z|)    
    ## (Intercept)  1.408874   0.054179  26.0042 < 2.2e-16 ***
    ## BSECBSEC2   -0.487134   0.071649  -6.7989 1.054e-11 ***
    ## BSECBSEC3   -0.055125   0.064215  -0.8585   0.39064    
    ## BSECBSEC4   -0.108108   0.062361  -1.7336   0.08299 .  
    ## BSECBSEC5   -0.069888   0.079575  -0.8783   0.37980    
    ## BSECBSEC6   -0.599137   0.069668  -8.5999 < 2.2e-16 ***
    ## BSECBSEC7   -0.764239   0.067277 -11.3597 < 2.2e-16 ***
    ## BSECBSEC8   -0.653992   0.078939  -8.2848 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The default error structure output for AR(1) models:

    error_structure(res_AR1_probit)

    ## (Intercept)   BSECBSEC2   BSECBSEC3   BSECBSEC4   BSECBSEC5   BSECBSEC6 
    ##  1.40887376 -0.48713415 -0.05512540 -0.10810818 -0.06988803 -0.59913737 
    ##   BSECBSEC7   BSECBSEC8 
    ## -0.76423929 -0.65399207

Correlation parameters ρ i for each firm are obtained by choosing type =
"corr"

    head(error_structure(res_AR1_probit, type = "corr"), n = 3)

    ##   Correlation
    ## 1   0.8749351
    ## 2   0.6694448
    ## 3   0.8749351

Correlation matrices for each specific firm are obtained by choosing
type = "sigmas"

    head(error_structure(res_AR1_probit, type = "sigmas"), n = 1)

    ## [[1]]
    ##           year1     year2     year3     year4     year5     year6
    ## year1 1.0000000 0.8749351 0.7655115 0.6697729 0.5860078 0.5127188
    ## year2 0.8749351 1.0000000 0.8749351 0.7655115 0.6697729 0.5860078
    ## year3 0.7655115 0.8749351 1.0000000 0.8749351 0.7655115 0.6697729
    ## year4 0.6697729 0.7655115 0.8749351 1.0000000 0.8749351 0.7655115
    ## year5 0.5860078 0.6697729 0.7655115 0.8749351 1.0000000 0.8749351
    ## year6 0.5127188 0.5860078 0.6697729 0.7655115 0.8749351 1.0000000
    ## year7 0.4485957 0.5127188 0.5860078 0.6697729 0.7655115 0.8749351
    ## year8 0.3924921 0.4485957 0.5127188 0.5860078 0.6697729 0.7655115
    ##           year7     year8
    ## year1 0.4485957 0.3924921
    ## year2 0.5127188 0.4485957
    ## year3 0.5860078 0.5127188
    ## year4 0.6697729 0.5860078
    ## year5 0.7655115 0.6697729
    ## year6 0.8749351 0.7655115
    ## year7 1.0000000 0.8749351
    ## year8 0.8749351 1.0000000
