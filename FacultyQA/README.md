# Project: Development of a Faculty Quality assurance system for monitoring Lectures.
Goal: to monitor whether lecturers in the university are taking their lectures as schedule in the timetable and also to track level of completion os syllabus for each course.

## University Structure:
Undergraduate Degrees
1. 4 Years programmes (4 sessions)
2. 5 Years programmes (5 sessions)
3. 6 Years programmes (6 sessions)
4. 7 Years programmes (7 sessions)

Graduate
1. MSc (2 Years)
2. PhD (3 Years)
3. PGD (1 to 2 yers)
but in the graduate programmes, lectures only takes place in the first 1 year. the rest of the years would be for research.


## Semester base tracking
Each Session == 2 Semesters
for a 4 Years programmes:
 - 100 Level (first semester, second semester) --> Session name: 2022/2023
 - 200 Level (first semester, second semester) --> Session name: 2023/2024
 - 300 Level (first semester, second semester) --> Session name: 2024/2025
 - 400 Level (first semester, second semester) --> Session name: 2025/2026

## Lecture Schedule
- Weekly based lectures (This means every course has a lecture schedule in a week until the end of the semester)
- A course may have more than one schedule in a week (e.g 
	A. 1 Credit Unit Course has 1 schedule of 1hr
	B. 2 Credit Unit Course has 1 schedule of 2hrs
	C. 3 Credit Unit Course has 1 schedule of 3hrs or 2 schedules of 2hrs and 1hr)
	
## Course Allocation
Avaialbale course allocation options
- 1 Course to 1 lecturer
- morethan 1 course to 1 lecturer
- 1 course to 2 lecturers

### Lecture schedule for: 1 course to 2 lecturers
- Weekly alternate lecture schedule (Lecturer A takes a week, lecturer B takes the following week)
- Seequential weeks schedule (e.g Lecturer A takes the first half of the weeks in a semester, while lecturer B takes takes the second half)
- Weekly concurrent lecture schedule (Both lecturers have schedule for same course every week) - this is less common

## Important notes
- The tracking must happen on semester basis
- New lectures time table is created the beginning of every Semester
- The system must work on semester(per session) bases, such that new tracking is done every semester
- previous semesters (per session) report properly preserved and can be filtered efficiently

## Report
Report is generated on:
- semester base
- session base
- department base
- faculty base
- university base


## User roles:
 0. Director Academic Planning (Supper admin role)
	- Create/manage Faculties
	- Assign/update Deans (one at a time. Maintain data integrity when Deans are changed)
	- Oversees the entire university
	- Generate University based report
 1. Dean Role:
	- Create/manage Departments
	- Assign/update Departments (one at a time. Maintain data integrity when HoDs are changed)
	- Oversees the entire Faculty
	- Generate Faculty Based report (Including for all deparyments in the faculty)
	
2. HoD Role:
	- Oversee his department
	- Create/upload courses (Code, Title, Credit Unit) - Done once and re-use repeatedly unless a new course is created or removed.
	- create/upload course syllabus (Each Course have list of topics/areas to be covered in a semester). Done once and re-used repeatedly unless course content is reviewed.
	- Assign Courses to Lecturers (A course may have morethan 1 lecturer, concurent weekly lectures on sequential) - Repeated task every semester.
	- View and generate Quality assurance report at department level - done at any time. Can generate report for current or previous semesters/sessions.
	
 3. Class Reps:
	- input lectures time table for his class 
		1. course
		2. days/time
		
	- mark attendance for every lecture (Time in/out)
	- Mark Topic(s), Module(s) covered for every lecture (preselect form existing record)
	- mark as postponed for the a lecture that has been posponded and the system must keep track
	- Mark absent for a missed lecture


## Trivial issues
The system relies on class reps for tracking whether a lecture has hold or not:
- Class reps may be compromised
- Class rep may be absent and the class has actually taken place
- Any other reason that may compromised the system.

To address this issues, I am suggesting the Class rep approach + aggregate voting from the class members. Thought I haven't figured out how that will work. I would need you to provided an effective solution.