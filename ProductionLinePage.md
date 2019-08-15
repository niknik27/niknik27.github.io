# Unity-as-a-production-line-simulator
A project I made in 2 weeks using Unity to create a simulation of a production line for doors and windows

## Motivation
This was created as a coding test for an interview. I incredibly enjoyed creating this project because I had to learn how to 
create and manage threads. I was also curious if I would be able to create this project on Unity because it isn't very thread friendly 
and is not necessarily designed for how I envisioned the project.

## Build status
[![Build Status](http://img.shields.io/travis/badges/badgerbadgerbadger.svg?style=flat-square)](https://travis-ci.org/badges/badgerbadgerbadger)

## Preview
<img src="/gifs/ProductionSimulator.gif" width="100%">

## Screenshots
<img src="/images/ProductionLineScreenshots/Screenshot.png?raw=true" width="100%" alt = "screenshot 1">

## Tech/framework used
<b>Built with</b>
- [Unity](https://unity.com/)

## Features
  - Multi-threaded application
  
  - Door measurements are randomly generated to simulate orders
  
  - Calculates height and width of the window using door measurements. Windows are calculated differently depending on 3 different window types.
  
  - Constantly calculates the average measurements of finished doors and windows after each new addition
  
  - The speed of the lasers and products can be changed during runtime
  
  - Generates a report in a .txt file that lists each product information as well as the final averages of the measurements

## Code Sample
<b>Method to calculate window measurements using given door measurements</b>

```C#
/// <summary>
    /// Gets all doors and matches each door with their corresponding window using their IdNumber
    /// The measurements are then calculated by:
    ///     *Getting the height and width of the door
    ///     *Subtracting the difference to create a gap
    ///     *Do calcuations depending on the selected window type
    /// </summary>
    public void calculateWindowMeasurements()
    {

        foreach (Door door in allDoors)
        {

            foreach (Window window in allWindows)
            {

                if (door.getIdNum() == window.getIdNum())
                {
                    if (door.getSelectedWindowType().Equals("Full"))
                    {
                        //calculates height of a full window by subtracting the height of door from the gaps 
                        //multiplied by 2 to account for both top and bottom gaps
                        windowHeight = door.getDoorHeight() - (heightDifference * 2);

                        //calculates width of a full window by subtracting the width of door from the gaps 
                        //multiplied by 2 to account for gaps on both sides
                        windowWidth = door.getDoorWidth() - (widthDifference * 2);

                        //set the window measurements
                        window.setWindowHeight(windowHeight);
                        window.setWindowWidth(windowWidth);

                    }
                    else if (door.getSelectedWindowType().Equals("Half"))
                    {
                        //calculates height of a half window by dividing the height of door by 2 and subtracting the gap
                        windowHeight = (door.getDoorHeight() / 2) - heightDifference;

                        //calculates width of a full window by subtracting the width of door from the gaps 
                        //multiplied by 2 to account for gaps on both sides
                        windowWidth = door.getDoorWidth() - (widthDifference * 2);

                        //set the window measurements
                        window.setWindowHeight(windowHeight);
                        window.setWindowWidth(windowWidth);

                    }
                    else if (door.getSelectedWindowType().Equals("Quarter"))
                    {
                        //calculates height of a quarter window by dividing the height of door by 4 and subtracting the gap
                        windowHeight = (door.getDoorHeight() / 4) - heightDifference;

                        //calculates width of a full window by subtracting the width of door from the gaps 
                        //multiplied by 2 to account for gaps on both sides
                        windowWidth = door.getDoorWidth() - (widthDifference * 2);

                        //set the window measurements
                        window.setWindowHeight(windowHeight);
                        window.setWindowWidth(windowWidth);
                    }
                    else
                    {

                    }

                    //print(window.getId() + "\nHeight:" + window.getWindowHeight() + "\nWidth:" + window.getWindowWidth() + "\nWindow Type:" + door.getSelectedWindowType());
                }
                else
                {

                }
            }
        }

        computationWindowDone = true;
    }
```

## Projects
  1. <a href="/50sPage">50's Diner Themed Website</a>
  2. <a href="/GamePage">Tiny Planet Defender</a>
  3. <a href="/SchoolManagerPage">School Manager Android Application</a>
  4. <a href="/InventoryManagerPage">Inventory Manager Java Application</a>
  5. <a href="/AppointmentManagerPage">Appointment Manager Java Application</a>
  6. <a href="/ProductionLinePage">Unity as a Production Line Simulator</a>

Copyright 2019 © [niknik27](https://github.com/niknik27)
