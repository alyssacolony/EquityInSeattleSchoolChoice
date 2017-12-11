
# DATA 512 Final Project: README File

## Does Seattle's School Choice System offer equal access to students regardless of race and socioeconomics?
Alyssa Goodrich  
December 10, 2017

## Abstract:
With the advent of Donald Trump's appointment of Betsy Devos, a long-time school choice advocate as the Secretary of Education, there is a national effort to increase access to school choice. Proponents of this system believe that students benefit from being able to choose the school that best meets their individual needs, which results in better achievement and attainment. Opponents of this system are concerned that it benefits only a certain group of students, while leaving out groups of marginalized students resulting in increased segregation and worse outcomes for some students, This paper investigates Seattle's school choice system and addresses the following questions: 
- **1.** Do Seattle's Choice schools serve all student groups equally?  
- **2a.** Does the admission prioritization system benefit student in the geozone to the detriment of children outside the geozone?  
- **2b.** Do admissions prioritization based on geozone disproportionately benefit any group of students?  
- **3.** Do students who attend Choice Schools perform better than their peers who attend attendance area schools (as measured by standardized testing conducted by the state)?  

We find that Seattle's school choice system disproportionately serves White students and Native American Students, while under-serving black, Hispanic, Asian and Low income students. We also find that the admission system favors white students because white students disproportionately live in the geozone areas. Finally, we find that there is mixed results on whether choice schools increase student' achievement. For students overall there is not a significant difference between achievement at choice schools vs attendance area schools. However, Hispanic students had higher rates of achievement at choice schools, while black and white students had higher rates of achievement at attendance area schools. The disproportionate access of white students to choice schools may warrant advocacy for a policy change in Seattle's school choice admission process. The achievement rates at choice and attendance area schools warrants more study. 

## Objective:  
The objective of this notebook is to introduce and explore our research questions outlined above and report on our findings and implications in a manner that is transparent and reproducible. The notebook includes the following sections: 
- Abstract: Brief summary of report and findings
- Introduction
- Background and related work: Provides context for the research questions studies
- Methods: Outlines analytical methods used, and human-centered data science considerations
- Findings: Code to execute analysis, along with descriptions of tasks completed by code, visualizations of results, and description of outcomes. 
- Discussion/Implications: Outlines implications of findings, limitations of the study, and opportunities for further research.
- Conclusions
- References

## Data Sources Used

There are two primary sources of data:  
**Source 1:** Seattle Public School District Website: which provides information on the following: 

    - Names of geozone schools 
        Found on this page http://www.seattleschools.org/admissions/school_choice (lower right corner)
    - Names and locations of all schools: Saved in file called 'Map_Elementary Attendance Areas.pdf'
        Found on this page http://www.seattleschools.org/UserFiles/Servers/Server_543/File/District/Departments/Enrollment%20Planning/Maps/boundarymaps/2017-18/district/2017_18_AA_ES.pdf
    - Locations of geozone areas: Saved in file called: 'SPSGeozones_17_18.pdf'  
        Found on this page: http://www.seattleschools.org/UserFiles/Servers/Server_543/File/District/Departments/Enrollment%20Planning/Maps/boundarymaps/2017-18/SPSGeozones_17_18.pdf
        

**Preparation required:** These reports are published as PDF and require manual processing to turn them into data files.
I conducted the following actions to turn these PDFs into data files:
    1. I reviewed the maps and lists and captured all school names and information on whether each school was a choice school or attendance area school
    2. I reviewed the map and identified attendance areas that overlapped with geozones
    3. I inserted into a file called "Name&Type1.csv" with the following fields:   
        * School: String: name of school
        * Type: String: (Attendance Area or Choice)
        * GeozoneOverlap: Num (0 for no geozone overlap, 1 for geozone overlap)


Seattle Public Schools also provided information on admission rate for students based on tiebreaker status (sibling, geozone) http://www.seattleschools.org/UserFiles/Servers/Server_543/File/District/Departments/Enrollment%20Planning/Reports/Annual%20Enrollment/2016%20Open%20Enrollment%20School%20Choice%20Data.pdf
    
**Preparation required:** These reports are published as PDF and require manual processing to turn them into data files.
I conducted the following actions to turn these PDFs into data files:
1. I extracted the data using a combination on of web PDF extraction tools  
2. I inserted into a file called "SibGeozoneAcc.csv" with the following fields:   
    * School: String: name of school
    * Geozone-Accepted: Int: # of students accepted with geozone status (Calculated as sum of students with geozone and sibling priorty and students with only geozone priority)
    * No Geozone-Accepted: Int: # of student acccepted with no geozone status  (Calculated as sum of students with sibling priority and "no tiebreaker" students)
    * Geozone-Waitlist: Int: Number of students with geozone status waitlisted
    * No geozone-Waitlist: Int: Number of students with geozone status waitlisted Calculated as sum of students with sibling priority and "no tiebreaker" students)	
    * No Geozone Applied: Int: Number of students with no geozone status waitlisted (calculated as sum of no geozone students who were accepted plus number who were waitlisted)	
    * Geozone Applied: Int: Number of students with geozone status who applied (calculated as sum of geozone students who were accepted plus number who were waitlisted)	

There are no available terms of use on the Seattle Public School district website, however the City of Seattle's data policy, found here: https://data.seattle.gov/stories/s/Data-Policy/6ukr-wvup/

The copyright for data files created from the information contained in the Seattle Public Schools website is held by Alyssa Goodrich and is released under an MIT license.


**Source 2**: . Office of Washington State Super Intendant of Public Instruction (OSPI)
    - How students achievement levels for various racial and economic groups, by school: 
            - This file includes: information on student test scores for the Smarter Balanced Assessment for all schools in the State of Washington. It is broken down into racial and socioeconomic groups. 
            - This file can be found at: http://reportcard.ospi.k12.wa.us/Reports/2017/2_03_AIM-EOC-MSP-SBA%20Assessments%20School%20(with%20suppression%20-%20new%20format).xlsx
            - Saved in file: '1_2_Demographic Information by School.csv'

    - Demographic data by school:
        - This file includes information for each school in the state, including total enrollment, and enrollment numbers for various student groups including different races and socioeconomic status (as measured by number of student recieving free and reduced price meals)
        - This file can be found at: 
        http://reportcard.ospi.k12.wa.us/Reports/2017/1_2_Demographic%20Information%20by%20School.xlsx
        - Saved in file: 'Demographic Information by School.csv'

Release granted by the State of Washington Open Data Policy:  
https://www.ocio.wa.gov/programs/open-data  
Open Data definitions  
https://www.ocio.wa.gov/programs/open-data/guidance-open-data-definitions  

## Resources used
This analysis was prepared using R running in a Jupyter Notebook environment.  

Documentation for R can be found here:https://www.r-project.org/other-docs.html 
Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/  

The following R packages were used and their documentation can be found at the accompanying links:  
- tidyr was used to clean and reshape data https://cran.r-project.org/web/packages/tidyr/tidyr.pdf
- dplyr was used to create and work with datatables https://cran.r-project.org/web/packages/dplyr/dplyr.pdf
- ggplot2 was used to create visualizations https://cran.r-project.org/web/packages/ggplot2/ggplot2.pdf
- IRdisplay was used to display images in Jupyter https://www.rdocumentation.org/packages/IRdisplay/versions/0.4.4

Data was extracted from PDF using Tabula, a free software package. Read more or download it here: http://tabula.technology

## Files Created
This notebook creates three CSV files of data extracted and compiled as part of this analysis.   

**File 1**
- File name: "DemographicInfo.csv"
- Fields included:
    - School, str
    - TotalEnrollment, int
    - NumberAmericanIndianorAlaskanNative, int	
    - NumberAsian, int
    - NumberBlack, int
    - NumberHispanic, int
    - NumberWhite, int
    - NumberFreeorReducedPricedMeals, int
    - Type str
    - GeozoneOverlap, binary (0 or 1)  
    
    
**File 2**
- File name: "AcceptRates.csv"
- Fields included:
    - School, str
    - Geozone.Accepted, int
    - No.Geozone.Accepted, int
    - Geozone.Waitlist, int
    - No.geozone.Waitlist, int
    - No.Geozone.Applied, int
    - Geozone.Applied, int
    - Type, str
    - GeozoneOverlap binary (0 or 1)  
    
    
**File 3**
- File name: 'AchievementInfo.csv'
- Fields included:
    - School, str
    - GradeLevel, str
    - StudentGroup, str
    - countMetStandardWithoutPP, int
    - countNotMet, int
    - Type, str
    - GeozoneOverlap, binary (0 or 1)
