# Dataproject: Prediction of craniofacial growth and occlusion for cleft lip and palate patients


## Table of contents
* [introduction](##introduction)
* [Goals](##Goals)
* [model](#model)

# Introduction (kopi basted aflevering)(malthe)  
Cleft lip and palate is the most common with-born disease. It appears in approximately 0.02% of all new-borns. The cleft of the lip and palate is surgically closed in early childhood (primary surgery) and
it is well-known, that this surgery creates scar tissue which might influence growth of the maxillofacial
complex as well as occlusion (bite). This study is part of a multicentre prospective, randomised,
controlled clinical trial studying non-syndromic Caucasian children with unilateral cleft lip and palate,
which evaluated timing and method of the primary surgery in 450 patients. In Trial 1, which the Aarhus
group belongs to, the surgical variable was timing. All patients received surgical closure of the lip at 3
months of age; then, half of the patients received closure of the palate at 1 year of age (group A) and
the other half at 3 years of age (group B). The outcome we want to look at is craniofacial growth and
occlusion.
The Aarhus material consists of 84 patients followed from birth to 21 years of age. Patients received
orthodontic treatment at the age of 8 (OR I) in the mixed dentition before they received secondary
surgery for closure of the cleft in the alveolar process. When the patients were in the permanent
dentition a second orthodontic treatment (OR II) was performed. Lateral cephalograms and dental
casts were taken before (age 12) and after (age 16) this orthodontic treatment. At 16 years and after
OR II the patient is considered at the end of treatment and occlusion and growth can be evaluated.
Occlusion is evaluated on the study models taken at age 8, 12 and 16 with two different scoring systems
[Goslon (score 1-5) and Pinheira (score 0-52)]. Craniofacial growth was evaluated by assessing specific
angles between anatomical landmarks on cephalometric radiographs.
The aim of this project is to assess whether the abovementioned measurements at age 8 can be used
to predict the craniofacial growth and occlusion at a later age. It involves the analysis and evaluation
of several predictive models on tabular data, with a particular focus on explainability of the model.

## goals 
The overall goal for this project is to create a way for dentist to estimate the final Pinheria score, from the initial measurement.
## Problems
The first problem we found was the data with a $n=123$ it is difficult to create a neural network, also we didnt find any visible depence within the data.

# First hand findings
<img width="1429" alt="Skærmbillede 2024-03-18 kl  13 11 03" src="https://github.com/Christofferfuglkjaer/Dataproject/assets/118052934/f9c3827a-b53d-48bf-817c-38a9ac89fd15">

# Model 

## hvilken model bruger vi, og hvorfor (Christoffer)
Vi har valgt at bruge en logistisk regression, denne model blev valgt fordi vi ønskede at lave en binear klassificering, og med den mængde data vi har, gav det mening at bruge en supervised model. 

## hvad indebærer modellen og hvordan virker den i praksis (Chrizz)

Vi bruger modellen, ved at lave en binear variable som bare er 1 hvis resultatet er godt og 0 hvis det ikke er, da vil den forudsigelse som vores model laver, være en sandsynlighed for at ligge i en af de to klasser. \
Den logistiske model er opskrevet således $$p(x) = \frac{1}{1+e^{-(x-\mu)/s}}$$ Hvor $\mu$ er det sted hvor $p(x) = \frac{1}{2}$ ## måske gennemgå det her sammen, da det er ret tung teori.\

I jupyter notebook filen 'Logistic-regression-model' bruger vi Sklearn pakken til vores model. Helt generelt så importere vi det allerede opryddet data, da standardiserer vi data og opretter vores binær kolonne. Dernæst splitter vi data op i $75 \%$ trænings data og $25\%$ test data. Nu kan vi træne vores model og bagefter bruge test data til at få hvor "god" vores model er, vi laver også en confusion matrix og en klassificerings report for bedre at kunne se, hvordan vores modellen gætter. Da vi havde store svingninger i vores models præcision, valgte vi at bruge en bootstrap tilgang, hvor vi kører modellen 25 gange og tager middelværdien af forudsigelse, præcision og SHAP værdierne. Det har gjort at vores model er mere stabil og giver en mere ensartet forudsigelse. 
 
## SHAP værdier og hvad bruger vi dem til. (Oswald)
SHAP (SHapley Additive exPlanations) er en metode, der kan bruges til at fortolke/forklare Machine Mearning modellers forudsigelser. Mere specifikt, kan man se hver parameters effekt på en forudsigelse.\
Når man arbejder med SHAP-værdier, er det vigtigt at notere sig, at de ikke kan bruges til at forklare kausalitet. Siger udelukkende noget om, hvordan modellen er kommet frem til en forudsigelse/resultat.\
\
Vi bruger to plots fra pakken 'shap', til forklare modellens forudsigelser. De kan findes under 'Extra Information' i streamlit appen. Her kan man se, at de fleste gange modellen bliver kørt, vil Antereoposterior 1.1 være den parameter med størst effekt. På det andet plot ses, hvor uforudsiglig problemstillingen egentlig er - der er ikke stor sammenhæng mellem parameter-værdien og shap-værdien. (Optimalt ville røde og blå punkter være adskilt).\

https://www.datacamp.com/tutorial/introduction-to-shap-values-machine-learning-interpretability

## problemer 

# andre tilgange ()
## neural network (Christoffer)
Inden vi valgte at bruge en logistisk regression, blev muligheden for et neuralt netværk udforsket, dette tog lang tid og endte ud i det vi  fra starten lidt havde forudsagt. Vi har simpelthen ikke nok data, og for mange variable. Men det gav os en bedre forståelse for hvodan et neuralt netværk virker, men vigtigste af alt, hvornår giver det mening at bruge et neuralt netværk. Vi endte lidt en i en blindgyde hvor modellen præcision ikke var særlig god, valgte vi at tage et skridt bagud og genoverveje hvordan vi ville takle dette projekt. 

## verdens bedste LM (Malthe)
## PCA og SVD. (Oswald)


# opnåede vi de mål? (team combo) 
## lave upload tamtam 
## Streamlit app (Christoffer)
Da vi gerne vil have at tandlægerne kan bruge den model vi har lavet som et værktøj, ønskede vi fra starten at gøre det så nemt som muligt for dem at indtaste nye tal og så få en forudsigelse tilbage. Her har vi brugt en python pakke som hedder Streamlit, som ligeledes hoster hjemmesiden i skyen for os. Det betyder at vi laver et slags dashboard, det gør det nemt for tandlægerne at bruge vores model uden at skulle installere python eller overhovedet forstå det tekniske bag vores model og forudsigelse. (Ligeledes er det muligt for dem at oploade mere data, som vores model så kan bruge i fremad.)\
Det har været vanskeligt og meget tid er langt i hjemmesiden, da vi skulle lære en hvordan Streamlit fungerer. Vi opfordre at man går ind og kigger på hjemmesiden. 
link til hjemmeside:  https://cleft-lip-app-r4y7280urvh.streamlit.app
