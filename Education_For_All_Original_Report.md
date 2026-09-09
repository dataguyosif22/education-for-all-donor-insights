## REPORT FOR CHARITY ON 

## EDUCATION FOR ALL 

 10Alytic internship Project 

#### Presented by Yusuf 

#### Tunde Dunmoye 


<!-- PAGE_BREAK -->
# Introduction 

This project involves presenting data insight of currently received donations from different 

donors. Two 

data sets from a charity organization (Education for All) were provided by the 10Alytic team, 

namely 

‘Donation data’ and ‘Donor data’, both of which contain different pieces of information related 

to donors’ biodata and their donations. 

In addition, the business problem is to devise strategies of increasing funds for Education for All 

charity 

organizations, using the provided data. Specifically, the tasks include increasing the number of 

donors, 

increasing the donation frequency, and the donation amount itself. 

All data were imported into the SQL tool (sqliteonline.com) using Postgres IDE and were 

queried with different codes to 

obtain insights necessary to increase donations. Importantly, wealth makers (real estates), 

business 

tycoons, loyal donors (daily-weekly-monthly), and people with luxurious lifestyles (exotic cars) 

were 

identified using various queries, while redundant and uneducated people who understand 

a second 

language provided a complete insight into possible targets of donation increment. Gender did not 

make 

any difference and donors were higher from certain states than others. 

Results showed that a low level of education and ability to speak a second language negatively 

affected 

donation. Almost all redundant donors did not have a university degree and consequently did not 

understand why they should support the charity cause. In addition, most of them may have preferred to receive correspondence from the organization from their second 

language and therefore did not respond well to emails and honor invitations. 


<!-- PAGE_BREAK -->
The fundraising team should consider sending emails to redundant donors in their 

second language. 

### Root Cause Analysis Process 

Problem: Find ways of increasing donors, donation frequency, and amount for education 

Why: Fewer donations, few donors, and redundancy in donation 

Why: A language barrier, wrong audience, and lack of motivation 

Why: Some donors understand a second language, have little 

education 

Why: Nature of their work/business, successful in other careers, apart from education 

### Insight from Analysis 

1. Total donors were 1000 of which 508 were females while 492 were males. The total sums of donations were calculated based on gender and it was found that a total of 

$121457 (48%) donors were female, using the sequel code below, while male donors were 

$127628 (52%) donors, making a total of $249085. The following SQL queries were used 

**Total donation and number of donations by gender** 

**SELECT** gender, **SUM** (donation), **COUNT** (donation) 

 FROM "Donation_Data" 

 GROUP BY gender; 

**Total donation amount** 

**SELECT SUM** (donation) 

**From** "Donation_Data"; 


<!-- PAGE_BREAK -->
2. The total donations per state were estimated, and values were accessed in the SQL queries below 

The top 10 states that donated the least (Fig.1) are Wyoming ($258), South Dakota ($401), North Dakota ($651), Alaska ($734), West Virginia ($793), South Carolina ($819), New Hampshire ($841), Hawaii ($875) and Montana ($1009). While the 10 states that donated the most (Fig. 2) are California ($30,264), Texas ($24097), Florida ($20562), New York ($14759), Virginia ($10750), Illinois ($8674), District of Columbia ($8376), Tennessee ($8316), Georgia ($8046) and Ohio ($6876) as shown below in Fig.1 and Fig. 2; 

**Top 10 States with least amount of donations** 

**SELECT** state, **SUM** (donation) **FROM** "Donation_Data" **GROUP BY** state **ORDER BY SUM** (donation) **ASC LIMIT** 10 ; 

 Fig.1 

**Top 10 States with the highest amount of donations** 

**SELECT** state, **SUM** (donation) **FROM** "Donation_Data" **GROUP BY** state **ORDER BY SUM** (donation) **DESC LIMIT** 10 ; 

 Fig.2 


<!-- PAGE_BREAK -->
3. Donors donated at different frequencies. The donation frequencies are; Once ($32,666), Weekly ($31,645), Daily ($29,249), Yearly ($35,266), Seldom ($30,650), Monthly ($26,870), Often ($28,476), and Never ($34,263). 

**Total donation by frequency of donation** 

**SELECT SUM** ("Donation_Data".donation),"Donor_Data".donation_frequency **FROM** "Donation_Data" **JOIN** "Donor_Data" **ON** "Donation_Data".ID = "Donor_Data".ID **GROUP BY** donation_frequency; 

4. Total numbers of donors who work in one of the 12 different job fields. They are Business Development (94), Human Recourses (93), Engineering (93), Product Management (90), Training (84), Research & Development (84), Sales (83), Accounting (80), Services (80), Support (79), Marketing (74), and Legal (66) 

Donors who work in Human Resources donated more money ($23,060) while those that work in Legal ($17309) donated the least. Fig. 3 

**SELECT** job_field, **SUM** (donation), **COUNT** (donation) **FROM** "Donation_Data" **GROUP BY** job_field; 


<!-- PAGE_BREAK -->
 Fig. 3 

5. Over ~50% (586) of the total numbers of donors donated over $200 with a total donation of $205,892 and ~41% (411) of donors donated less than $200 with a total donation of $24,593 while ~1% (3) donors donated $200 with a total donation of $600. 

**SELECT SUM** (donation), **COUNT** (donation) **FROM** "Donation_Data" **WHERE** donation >$200; Fig. 4 

**SELECT SUM** (donation), **COUNT** (donation) **FROM** "Donation_Data" **WHERE** donation <$200; Fig.5 

**SELECT SUM** (donation), **COUNT** (donation) **FROM** "Donation_Data" **WHERE** donation = $200; Fig.6 


<!-- PAGE_BREAK -->
6. Donation by donors’ car. Top 10 cars driven by donors that made the highest donation are; Ford ($22,706), Chevrolet ($19,875), Toyota ($14,123), GMC ($10,145), Mitsubishi ($10,001), Dodge ($9,479), Pontiac ($9,331), Honda ($9,201), Honda ($9,201), Volkswagen ($8,964) and BMW ($8,608). 

**SELECT** "Donor_Data".car, **SUM** ("Donation_Data".donation) **FROM** "Donation_Data" **JOIN** "Donor_Data" **ON** "Donation_Data".id = "Donor_Data".id **GROUP BY** "Donor_Data".car **ORDER BY SUM** ("Donation_Data".donation) **DESC LIMIT** 10; 

7. Donors who speak a second language by donation frequency. 

SELECT "Donor_Data".donation_frequency, COUNT("Donor_Data".second_language), SUM("Donation_Data".donation) 

 FROM "Donation_Data" 

 JOIN "Donor_Data" 

 ON "Donation_Data".id = "Donor_Data".id 


<!-- PAGE_BREAK -->
 GROUP BY "Donor_Data".donation_frequency 

 ORDER BY COUNT("Donor_Data".second_language)DESC; 

### Findings and Recommendations 

There is a direct relationship between the ability to speak a second language and the value/frequency 

of donation. Donors who could speak a second language probably preferred the second 

language to the first, and thus did not respond to emails or invitations to charity donations. Their 

job fields cut across many sectors and thus if they are in a country different from where the 

charity 

organization is situated and where another language they understand is spoken, there is a tendency 

that they will not respond to emails and invitations. 

It is, therefore, necessary for the charity organization to provide translation tools within the email 

for clients who may prefer to read their letters in a second language 

More email marketing strategies and physical representation are needed in states that recorded 

low donations. This will increase the donations received. In addition, more programs 


<!-- PAGE_BREAK -->
should be organized for loyal donors, who share the vision of the charity organization and donate 

daily, weekly, monthly, and yearly basis. Gift items should also be presented to them to show 

appreciation and renew their commitment. 

### Conclusion 

The data shows that ability to speak a second language and a low level of education can 

negatively affect the frequency and value of donations received.
