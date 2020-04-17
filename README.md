# Sophia-Villiere-Statistic-Part-4-17-20
> summary(fit)

Call:
lm(formula = log2(dispersion[, 2] + 1) ~ log2(dispersion[, 1] + 
    1))

Residuals:
    Min      1Q  Median      3Q     Max 
-5.9338 -0.8826 -0.1267  0.7914  3.8003 

Coefficients:
                          Estimate Std. Error t value Pr(>|t|)    
(Intercept)               0.890289   0.016322   54.54   <2e-16 ***
log2(dispersion[, 1] + 1) 1.731079   0.002061  839.75   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1.209 on 15347 degrees of freedom
Multiple R-squared:  0.9787,	Adjusted R-squared:  0.9787 
F-statistic: 7.052e+05 on 1 and 15347 DF,  p-value: < 2.2e-16

> confit(fit, level=.95)
Error in confit(fit, level = 0.95) : could not find function "confit"
> confint(fit, level=.95)
                              2.5 %    97.5 %
(Intercept)               0.8582948 0.9222822
log2(dispersion[, 1] + 1) 1.7270386 1.7351199
> > pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.8)
Error: unexpected '>' in ">"
> pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.8)

     Multiple regression power calculation 

              u = 4
              v = 3.318652
             f2 = 5.789599
      sig.level = 0.05
          power = 0.8

> pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.9)

     Multiple regression power calculation 

              u = 4
              v = 3.956176
             f2 = 5.789599
      sig.level = 0.05
          power = 0.9

> pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.7)

     Multiple regression power calculation 

              u = 4
              v = 2.886402
             f2 = 5.789599
      sig.level = 0.05
          power = 0.7

> pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.6)

     Multiple regression power calculation 

              u = 4
              v = 2.532914
             f2 = 5.789599
      sig.level = 0.05
          power = 0.6

> pwr.f2.test(u=f[2], v=NULL, f2=f2, sig.level=0.05,power=0.5)

     Multiple regression power calculation 

              u = 4
              v = 2.213508
             f2 = 5.789599
      sig.level = 0.05
          power = 0.5
res.UTMG_v_fra3 <- results(dds, contrast = c("condition", "fra3", "UTMG"))
res.UTMG_v_fra3 <- subset(res.UTMG_v_fra3, !is.na(res.UTMG_v_fra3$padj))
resSig.UTMG_v_fra3 <- res.UTMG_v_fra3[ abs(res.UTMG_v_fra3$padj) < .01, ]
resSig05.UTMG_v_fra3 <- res.UTMG_v_fra3[ abs(res.UTMG_v_fra3$padj) < .05, ]
resSig01.UTMG_v_fra3 <- res.UTMG_v_fra3[ abs(res.UTMG_v_fra3$padj) < 1, ]
resAll.UTMG_v_fra3 <- res.UTMG_v_fra3[ abs(res.UTMG_v_fra3$padj) < 2, ]
write.table(resSig.UTMG_v_fra3, file="UTMG_v_fra3_DESeq_refGene.FDR01.txt", quote=F, sep="\t", row.names=T)
write.table(resSig05.UTMG_v_fra3, file="UTMG_v_fra3_DESeq_refGene.FDR05.txt", quote=F, sep="\t", row.names=T)
write.table(resSig01.UTMG_v_fra3, file="UTMG_v_fra3_DESeq_refGene.FDR01.txt", quote=F, sep="\t", row.names=T)
write.table(resAll.UTMG_v_fra3, file="UTMG_v_fra3_DESeq_refGene.all.txt", quote=F, sep="\t", row.names=T)

plotMA(res.UTMG_v_fra3, alpha = .01,main="UTMG_v_fra3_FDR01")
plotMA(res.UTMG_v_fra3, alpha = 0, main="UTMG_v_fra3_FDR01")
plotMA(res.UTMG_v_fra3, alpha = .05,main="UTMG_v_fra3_FDR05")
plotMA(res.UTMG_v_fra3, alpha = .10,main="UTMG_v_fra3_FDR10")
hist(res.UTMG_v_fra3$pvalue, breaks=20, col="grey")
plot(res.UTMG_v_fra3$baseMean+1, -log10(res.UTMG_v_fra3$pvalue),log="x",xlab="mean of normalized counts",ylab=expression(-log[10](pvalue)),ylim=c(0,30),cex=.4,col=rgb(0,0,0,.3))

dev.off()

                
