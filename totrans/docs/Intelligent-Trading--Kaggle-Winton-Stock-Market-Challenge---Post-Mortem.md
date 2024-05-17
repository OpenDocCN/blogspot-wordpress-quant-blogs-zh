<!--yml
category: 未分类
date: 2024-05-18 04:43:45
-->

# Intelligent Trading: Kaggle Winton Stock Market Challenge - Post-Mortem

> 来源：[http://intelligenttradingtech.blogspot.com/2016/01/kaggle-winton-stock-market-challenge.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2016/01/kaggle-winton-stock-market-challenge.html#0001-01-01)

```
library(gbm)
library(doParallel)
library(reshape2)

#trn <- read.csv("E:/Kaggle/Winton/train.csv") # 40k X 211
#tst <- read.csv("E:/Kaggle/Winton/test_2.csv") #120k X 147

trn <- readRDS("E:/Kaggle/Winton/trn.rds"); tst <- readRDS("E:/Kaggle/Winton/tst.rds")

interp <- function(x){
x <- as.numeric(x)
if(is.na(x[1])) x[1] <- x[!is.na(x)][1]
#if(is.na(x[length(x)])) x[length(x)] <- x[length(x)-1]
xsub <- x[2:length(x)]
#gap.na <- which(is.na(xsub))

for(k in 2:length(xsub)){
if(is.na(xsub[k])) xsub[k] <- xsub[k-1] 
}
x <- c(x[1],xsub)
return(x)

}
disc.impute <- function(x){

xfactor <- levels(factor(x))
x[is.na(x)] <- sample(xfactor,length(which(is.na(x))),replace=TRUE)

return(as.numeric(x))
}
cont.impute <- function(x){

x[is.na(x)] <-
runif(length(which(is.na(x))),
min(range(na.omit(x))),max(range(na.omit(x))))

return(x)
}
generate.folds <- function(idx, k){

fold.idx <- holdout <- kfold <- list()
fold.len <- floor(length(idx)/k) # if idx does not divide evenly ignore last few observations

for(i in 1:(k-1)){
holdout[[i]] <- sample(idx[!(idx%in%unlist(holdout))],fold.len)
kfold[[i]] <- idx[!(idx%in%holdout[[i]])]
}
holdout[[k]] <- idx[!(idx%in%unlist(holdout))]
kfold[[k]] <- idx[!(idx%in%holdout[[k]])]

folds <- list(kfold,holdout)
names(folds) <- c('trn','val')

return(folds)
}
qlimiter <- function(x,qlim) {
ifelse(x < quantile(x,(1-qlim),na.rm=TRUE),quantile(x,(1-qlim),na.rm=TRUE),ifelse(
x > quantile(x,qlim,na.rm=TRUE),quantile(x,qlim,na.rm=TRUE),x))
}
feat.dist.sel <- function(mx,my,pth){
out <- 0
for(i in 1:dim(mx)[2]){
out[i] <- t.test(mx[,i],my[i])$p.value
}
sel <- which(out > pth)
return(sel)
}
interp.med <- function(x) {
x[is.na(x)] <- median(na.omit(x)); x
}

# column breakpoints
f1 <- 2; f25 <- 26; tsiis1 <- 27; tsiis2 <- 147; tsoos1 <- 148; tsoos2 <- 207;
tsD1 <- 208; tsD2 <- 209;
wtint <- 210; wtdly <- 211; trn.obs <- dim(trn)[1]; tst.obs <- dim(tst)[1];
clip.th <- 0.9999
discrete.features <- c(1,5,8,9,10,13,16,20)
continuous.features <- c(2,3,4,6,7,11,12,14,15,17,18,19,21,22,23,24,25)

# preprocess and clean data 
all.iis <- rbind(trn[,1:tsiis2], tst[,1:tsiis2])

all.trn.iis.ts <- trn[,tsiis1:tsiis2]
all.trn.oos.ts <- trn[,tsoos1:tsoos2]
all.trn.oos.ts.cln <- apply(all.trn.oos.ts,2,interp.med)

all.trn.oos.D1 <- trn[,tsD1]
all.trn.oos.D2 <- trn[,tsD2]
all.trn.oos.D1.clip <- qlimiter(all.trn.oos.D1,qlim=clip.th)
all.trn.oos.D2.clip <- qlimiter(all.trn.oos.D2,qlim=clip.th)

all.iis.ts <- all.iis[,tsiis1:tsiis2]
all.tst.iis.ts <- all.iis.ts[(trn.obs+1):(trn.obs+tst.obs),]

ts.sel <- feat.dist.sel(all.trn.iis.ts,all.tst.iis.ts,pth=.05)
all.iis.ts.sel <- all.iis.ts[,ts.sel]

all.iis.ts.cln <- apply(all.iis.ts.sel,2,interp.med)
all.trn.iis.ts.cln <- all.iis.ts.cln[1:trn.obs,]
all.tst.iis.ts.cln <- all.iis.ts.cln[(trn.obs+1):(trn.obs+tst.obs),]

# K FOLD CV
folds <- list(); n.fold <- 5
folds <- generate.folds(seq(dim(trn)[1]), n.fold)

#gbmGrid <- expand.grid(interaction.depth = c(5,9,15), n.trees = seq(400,1000,by=200),
#shrinkage = 0.1, n.minobsinnode = 50)
out <- res  <- list()
tune.par <- seq(10,200,10)

for(z in 1:length(tune.par)){
cl <- makeCluster(n.fold)
registerDoParallel(cl)

res <- list()
rmcol = 0

n.trees <- tune.par[z]
interaction.depth <- 1
n.minobsinnode  <- 50
shrinkage <- 0.1

res <- foreach(k=1:n.fold, .combine=rbind) %dopar% 
{

library(gbm)

trn.fld <- folds$trn[[k]]
val.fld <- folds$val[[k]]

# Naive estimates use zero baseline as predictions

trn.iis <- all.trn.iis.ts.cln[trn.fld,] ; val.iis <- all.trn.iis.ts.cln[val.fld,] 
trn.int.oos <- all.trn.oos.ts.cln[trn.fld,] ; val.int.oos <- all.trn.oos.ts.cln[val.fld,] 
trn.day.D1 <- all.trn.oos.D1.clip[trn.fld] ; val.day.D1 <- all.trn.oos.D1.clip[val.fld]
trn.day.D2 <- all.trn.oos.D2.clip[trn.fld] ; val.day.D2 <- all.trn.oos.D2.clip[val.fld]

wt.int.trn <- trn[trn.fld,wtint]; wt.int.val <- trn[val.fld,wtint]
wt.day.trn <- trn[trn.fld,wtdly]; wt.day.val <- trn[val.fld,wtdly]

trn.zro <- rep(0,dim(trn.iis)[1]); #zero pred for intraday
val.zro <- rep(0,dim(val.iis)[1]); #zero pred for intraday
trn.err.int <- wt.int.trn*abs(trn.int.oos-trn.zro) 
val.err.int <- wt.int.val*abs(val.int.oos-val.zro)
trn.err.D1 <- wt.day.trn*abs(trn.day.D1-trn.zro)
val.err.D1 <- wt.day.val*abs(val.day.D1-val.zro)
trn.err.D2 <- wt.day.trn*abs(trn.day.D2-trn.zro)
val.err.D2 <- wt.day.val*abs(val.day.D2-val.zro)

WMAE.trn <- mean(c(as.matrix(trn.err.D1),as.matrix(trn.err.D2),as.matrix(trn.err.int))) #oos trn wmae
WMAE.val <- mean(c(as.matrix(val.err.D1),as.matrix(val.err.D2),as.matrix(val.err.int))) #oos tst wmae
WMAE.zro.all <- mean(c(WMAE.trn,WMAE.val))

# feature selection and cleaning outliers
all.feat  <- all.iis[,f1:f25]
all.feat[,3] <- qlimiter(all.feat[,3],.9999)
all.feat[,11] <- qlimiter(all.feat[,11],.9999)
trn.feat <- all.feat[trn.fld,]
val.feat <- all.feat[val.fld,]

trn.day.1 <- data.frame(trn.feat,all.trn.iis.ts.cln[trn.fld,],all.trn.oos.D1.clip[trn.fld])
names(trn.day.1)[dim(trn.day.1)[2]]<-'D1'
trn.day.2 <- data.frame(trn.feat,all.trn.iis.ts.cln[trn.fld,],all.trn.oos.D2.clip[trn.fld])
names(trn.day.2)[dim(trn.day.2)[2]]<-'D2'

val.day.1 <- data.frame(val.feat,all.trn.iis.ts.cln[val.fld,],all.trn.oos.D1.clip[val.fld])
names(val.day.1)[dim(val.day.1)[2]]<-'D1'
val.day.2 <- data.frame(val.feat,all.trn.iis.ts.cln[val.fld,],all.trn.oos.D2.clip[val.fld])
names(val.day.2)[dim(val.day.2)[2]]<-'D2'

# Build gbm models, here: use same ntrees for both D1,D2
gbm.trn.mod.D1 <- gbm(D1 ~ .,data=trn.day.1,distribution="laplace",  weights = wt.day.trn, 
n.trees=n.trees, interaction.depth=interaction.depth, shrinkage = shrinkage, n.minobsinnode =n.minobsinnode)

gbm.trn.mod.D2 <- gbm(D2 ~ .,data=trn.day.2,distribution="laplace", weights = wt.day.trn, 
n.trees=n.trees, interaction.depth=interaction.depth, shrinkage = shrinkage, n.minobsinnode =n.minobsinnode)

# TRN fold predictions

gbm.trn.pred.1 <- predict(gbm.trn.mod.D1, newdata=trn.day.1[,-dim(trn.day.1)[2]], 
n.trees=n.trees)
gbm.trn.pred.2 <- predict(gbm.trn.mod.D2, newdata=trn.day.2[,-dim(trn.day.2)[2]], 
n.trees=n.trees)
gbm.trn.act.1 <- all.trn.oos.D1[trn.fld] 
gbm.trn.act.2 <- all.trn.oos.D2[trn.fld] 
#par(mfrow=c(2,1))
#plot(gbm.trn.pred.1~gbm.trn.act.1)
#plot(gbm.trn.pred.2~gbm.trn.act.2)

trn.err.day.1 <- wt.day.trn*abs(gbm.trn.act.1 -gbm.trn.pred.1)
trn.err.day.2 <- wt.day.trn*abs(gbm.trn.act.2 -gbm.trn.pred.2)
trn.err.dly <- data.frame(trn.err.day.1,trn.err.day.2)
trn.err.int <- trn.err.int # from previous median estimates, wt.int.trn*abs(trn.int.oos-trn.med) 
WMAE.trn <- mean(c(as.matrix(trn.err.dly),as.matrix(trn.err.int)))

# VAL fold predictions

gbm.val.pred.1 <- predict(gbm.trn.mod.D1, newdata=val.day.1[,-dim(val.day.1)[2]], 
n.trees=n.trees, interaction.depth=interaction.depth, shrinkage = shrinkage, n.minobsinnode =n.minobsinnode)
gbm.val.pred.2 <- predict(gbm.trn.mod.D2, newdata=val.day.2[,-dim(val.day.2)[2]], 
n.trees=n.trees, interaction.depth=interaction.depth, shrinkage = shrinkage, n.minobsinnode =n.minobsinnode)
gbm.val.act.1 <- all.trn.oos.D1[val.fld] 
gbm.val.act.2 <- all.trn.oos.D2[val.fld] 

#par(mfrow=c(2,1))
#plot(gbm.val.pred.1~gbm.val.act.1)
#plot(gbm.val.pred.2~gbm.val.act.2)

val.err.day.1 <- wt.day.val*abs(gbm.val.act.1-gbm.val.pred.1)
val.err.day.2 <- wt.day.val*abs(gbm.val.act.2-gbm.val.pred.2)
val.err.dly <- data.frame(val.err.day.1,val.err.day.2)
val.err.int <- val.err.int # from previous median estimates, wt.int.trn*abs(trn.int.oos-trn.med) 
WMAE.val <- mean(c(as.matrix(val.err.dly),as.matrix(val.err.int)))

res[[k]] <- data.frame(k,interaction.depth,n.trees,shrinkage,n.minobsinnode,WMAE.zro.all,WMAE.trn,WMAE.val)

}

out[[z]] <- t(do.call(rbind,res))
stopCluster(cl)
gc()
}

# aggregate and plot data
{
out.folds <- do.call(rbind,out)
mean.res <- aggregate(cbind(WMAE.zro.all,WMAE.trn,WMAE.val)~n.trees,data=out.folds,mean)

plot(mean.res$WMAE.trn~mean.res$n.trees,type='o',pch=19,col='red')
lines(mean.res$WMAE.val~mean.res$n.trees,type='o',pch=19,col='blue')

yr <- range(mean.res$WMAE.zro.all,mean.res$WMAE.trn,mean.res$WMAE.val)
plot(mean.res$WMAE.zro.all~mean.res$n.trees,type='o',col='blue',pch=19,ylim=yr,main=
'8 flds sweep',ylab='8 FOLD CV WMAE')
text(mean.res$WMAE.zro.all~mean.res$n.trees,cex=.8,col='black',pos=3,label = round(mean.res$WMAE.zro.all,2))
lines(mean.res$WMAE.trn~mean.res$n.trees,type='o',pch=19,col='green',ylim=yr)
text(mean.res$WMAE.trn~mean.res$n.trees,cex=.8,col='black',pos=3,label = round(mean.res$WMAE.trn,2))
lines(mean.res$WMAE.val~mean.res$n.trees,type='o',pch=19,col='red',ylim=yr)
text(mean.res$WMAE.val~mean.res$n.trees,cex=.8,col='black',pos=3,label = round(mean.res$WMAE.val,2))
legend(800,1*yr[2],c("mean.res$WMAE.zro","mean.res$WMAE.trn","mean.res$WMAE.val"),
col=c('blue','green','red'),pch=19)

dev.new()

CV.df <- out.folds[,c(3,c(6:8))]
CV.df <- transform(CV.df,ID=seq(dim(CV.df)[1]))

df.m <- melt(CV.df, id.var=c('ID','n.trees'))
boxplot(value~variable+n.trees,df.m)
}

############################################################
##########    FINAL all TRN model generate/WMAE
############################################################

n.trees <- 900
interaction.depth <- 1
n.minobsinnode  <- 50
shrinkage <- 0.1

all.feat  <- all.iis[,f1:f25] #limit useless or sparse feature outliers

all.feat[,3] <- qlimiter(all.feat[,3],.9999)
all.feat[,11] <- qlimiter(all.feat[,11],.9999)
trn.feat <- all.feat[1:trn.obs,]

trn.day.1 <- data.frame(trn.feat,all.trn.iis.ts.cln,all.trn.oos.D1.clip)
names(trn.day.1)[dim(trn.day.1)[2]]<-'D1'
trn.day.2 <- data.frame(trn.feat,all.trn.iis.ts.cln,all.trn.oos.D2.clip)
names(trn.day.2)[dim(trn.day.2)[2]]<-'D2'

trn.day.1 <- data.frame(trn.feat,all.trn.oos.D1.clip)
names(trn.day.1)[dim(trn.day.1)[2]]<-'D1'
trn.day.2 <- data.frame(trn.feat,all.trn.oos.D2.clip)
names(trn.day.2)[dim(trn.day.2)[2]]<-'D2'

wt.day.trn <- trn[,wtdly]

gbm.trn.mod.D1 = gbm(D1 ~ .,data=trn.day.1, distribution="laplace",weights = wt.day.trn,n.trees=n.trees,shrinkage=0.1 ,cv.folds=5)
gbm.trn.mod.D2 = gbm(D2 ~ .,data=trn.day.2, distribution="laplace",weights = wt.day.trn,n.trees=n.trees,shrinkage=0.1 ,cv.folds=5)

############################################################
##########   OOS TST GENERATE
############################################################

tst.feat <- all.feat[(1+trn.obs):dim(all.feat)[1],]

tst.day.1 <- data.frame(tst.feat,all.tst.iis.ts.cln)
tst.day.2 <- data.frame(tst.feat,all.tst.iis.ts.cln)

all.oos.int.pred <- sapply(all.trn.oos.ts,median,na.rm=TRUE)
tst.pred.mtx <- t(matrix(rep(all.oos.int.pred,dim(tst)[1]),
length(all.oos.int.pred),dim(tst)[1]))

gbm.tst.pred.1 <- predict(gbm.trn.mod.D1, newdata=tst.day.1, 
n.trees = n.trees)
gbm.tst.pred.2 <- predict(gbm.trn.mod.D2, newdata=tst.day.2, 
n.trees = n.trees)

tst.submission.mtx <- cbind(tst.pred.mtx,gbm.tst.pred.1,gbm.tst.pred.2)
tstpred <- as.vector(t(tst.submission.mtx))

submission <- read.csv("E:/Kaggle/Winton/sample_submission_2.csv")
submission$Predicted <- tstpred
write.csv(submission,"E:/Kaggle/Winton/submission1.csv",row.names=FALSE)
subtst <- read.csv("E:/Kaggle/Winton/submission1.csv")
```