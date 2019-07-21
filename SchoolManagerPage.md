# School-Manager-Android-Application
This is a small mobile application that can keep track of a student's courses, tests, and terms. 
It also provides a note taking feature.

## Preview
<img src="/gifs/SchoolManager.gif" width="100%">

## Tech/framework used
<b>Built with</b> [Android Studio](https://developer.android.com/studio)

<b>Using: </b>
  - Java
  - XML

## Screenshots
<img src="/images/SchoolManagerScreenshots/AndroidScreenshot1.png?raw=true" width="40%" alt = "screenshot 1">

<img src="/images/SchoolManagerScreenshots/AndroidScreenshot2.png?raw=true" width="40%" alt = "screenshot 2">

<img src="/images/SchoolManagerScreenshots/AndroidScreenshot3.png?raw=true" width="40%" alt = "screenshot 3">

## Features
  > Note taking features
  
  > Persistent saving using a SQLite database
  
  > Ability to add, edit, and delete Terms, Courses, and Assessments
  
  > Notifications and Alerts
  
  > Ability to enable and disable notifications and alerts
  
## Code Samples
<b>1. Method to access database and return a specific object</b>
```Java
public CourseAndMentor returnCourseAndMentor(){

        ArrayList<CourseAndMentor> selectedCourseAndMentor = new ArrayList<CourseAndMentor>();
        String courseName = CourseAndMentor.getSelection();
        CourseAndMentor selectedCourseAndMentorObjectReturn = null;

        if(!courseName.equals("")){

            selectedCourseAndMentor = readCourseAndMentorObjects("SELECT courseId, Course_tbl.termId, Course_tbl.mentorId, \n" +
                                                                        "\t\t\t\tcourseTitle, Course_tbl.startDate, Course_tbl.endDate,                                                                         \n" +
                                                                        "\t\t\t\t\ttermTitle, status, Course_tbl.alertActive,                                                                                    mentorName, phone, email\n" +
                                                                        "FROM Course_tbl, Mentor_tbl, Term_tbl\n" +
                                                                        "WHERE Course_tbl.termId = Term_tbl.termId\n" +
                                                                        "AND Course_tbl.mentorId = Mentor_tbl.mentorId\n" +
                                                                        "AND courseTitle = \"" + courseName + "\"");

            for (CourseAndMentor courseAndMentor : selectedCourseAndMentor){

                selectedCourseAndMentorObjectReturn = courseAndMentor;


            }
        }else{

            String TAG = "nullLog";
            Log.d(TAG, "Mentor Selection is EMPTY");
        }



        return selectedCourseAndMentorObjectReturn;
    }
```
<b>2. Method to access database and return a string matching a different string</b>

```Java
public String getMatchTermName(String columnName, String date){

        SQLiteDatabase db = this.getWritableDatabase();
        Cursor cursor = db.rawQuery("SELECT termTitle \n" +
                "FROM Term_tbl \n" +
                "WHERE " + columnName + " = \"" + date + "\"", null);

        String matchingTermName = "";

        while(cursor.moveToNext()){

            matchingTermName = cursor.getString(cursor.getColumnIndex("termTitle"));

        }

        return matchingTermName;

    }
```
<b>3. Method to access database and update a record in the "assessment" table</b>

```Java
 public long updateRecordAssessmentTbl(int assessID, int courseID, String name, String type, String goalDate,
                                          String startDate, String endDate, String whereClause, String[] whereArgs){

        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues values = new ContentValues();

        values.put("assessmentId", assessID);
        values.put("courseId", courseID);
        values.put("name", name);
        values.put("type", type);
        values.put("goalDate", goalDate);
        values.put("startDate", startDate);
        values.put("endDate", endDate);

        return db.update("Assessment_tbl", values, whereClause, whereArgs);

    }
```


Copyright 2019 © [niknik27](https://github.com/niknik27)
