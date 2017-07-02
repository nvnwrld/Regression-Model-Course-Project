data(mtcars)
mtcars$am[mtcars$am==0]<-"Automatic"
mtcars$am[mtcars$am==1]<-"Manual"
mtcars$am<-as.factor(mtcars$am)
mtcars$cyl<-as.factor(mtcars$cyl)
mtcars$vs<-as.factor(mtcars$vs)
mtcars$gear<-as.factor(mtcars$gear)
mtcars$carb<-as.factor(mtcars$carb)
str(mtcars)
boxplot(mtcars$mpg~as.factor(mtcars$am),col="blue",ylab="mpg",xlab="am",main="MPG vs AM")
t.test(mpg~am,mtcars,paired=FALSE,var.equal=FALSE)
basic<-lm(mpg~am,mtcars)
summary(basic)
full<-lm(mpg~.,mtcars)
fit<-step(full, direction="backward")
summary(fit)
anova(basic,fit)
par(mfrow=c(2, 2))
plot(fit)
