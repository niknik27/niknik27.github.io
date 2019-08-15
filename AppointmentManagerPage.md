# Appointment-Manager
This is a java application manages a consultant's appointments with their customers

## Motivation
This was created as a school project to show proficiency in java and fxml programming using Netbeans, as well as to practice accessing an online database.

## Tech/framework used
<b>Built with</b> [Netbeans IDE](https://netbeans.org/downloads/8.2/)

<b>Using: </b>
  - Java
  - FXML

## Screenshots

<img src="/images/ApmntManagerScreenshots/apnmtScreenshot1.png?raw=true" width="80%" alt = "screenshot 1">

<img src="/images/ApmntManagerScreenshots/apnmtScreenshot2.png?raw=true" width="40%" alt = "screenshot 2">

<img src="/images/ApmntManagerScreenshots/apnmtScreenshot3.png?raw=true" width="80%" alt = "screenshot 3">

<img src="/images/ApmntManagerScreenshots/apnmtScreenshot4.png?raw=true" width="80%" alt = "screenshot 4">

## Features
  > Simple User Interface
  
  > Persistent Data
  
  > Adds, edits, and deletes customer and appointment information
  
  > The administrator can see all appointmnets from all users
  
  > User input error prevention
  
  > User feedback prompts
  
## Code Sample
<b>Method to Access Database to Update using SQL through Java</b>

```Java
public void accessDBUpdate() {
        final String JDBC_DRIVER = "com.mysql.jdbc.Driver";
        final String DB_URL = "jdbc:mysql://52.206.157.109/U04XfS";

        //  Database credentials
        final String DBUSER = "U04XfS";
        final String DBPASS = "53688370542";

        Connection conn;
        boolean res = false;
        ResultSet rs = null;
                
        try {

            Class.forName("com.mysql.jdbc.Driver");

            System.out.println("Connecting to database...");
            conn = DriverManager.getConnection(DB_URL, DBUSER, DBPASS);

            Statement stmt;
            
            String insertAddress = "";
            String insertCity = "";
            String insertCountry = "";
            String insertCustomer = "";
            
            userName = LoginPageController.returnUName();
            
            insertCustomer = "INSERT INTO customer (customerId, customerName, customer.addressId, active, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custID + ", "
                                    + "'" + custName + "', "
                                    + "" + custAddressID + ", "
                                    + "" + custActive + ", "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
            
            caseCheck = cityAndCountryCheck();
            if(caseCheck == 1){//MEANS BOTH WERE EQUAL FROM EXISTING DATA
                
                //SET CITYID TO THE ONE EQUAL TO THE CITYNAME AND THE COUNTRY ID
                custCityID = cityIDFromLoop;
                //SET CITY.COUNTRYID TO THE ONE EQUAL TO THE COUNTRYNAME
                custCountryID = countryIDFromLoop;
                
                insertAddress = "INSERT INTO address (address.addressId, address, address2, address.cityId, postalCode, phone, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custAddressID + ", "
                                    + "'" + custAddress + "', "
                                    + "'" + custAddress2 + "', "
                                    + "" + custCityID + ", "
                                    + "'" + custPostalCode + "', "
                                    + "'" + custPhone + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
            }else if(caseCheck == 2){//MEANS CITY WAS EQUAL BUT COUNTRY WAS NOT
                
                 //ADD NEW ROW WITH AN AVAILABLE CITYID AND PLACE CITYNAME THERE
                custCityID = IDSelectionLoop("cityId" , "city");
                //ADD NEW ROW WITH AN AVAILABLE COUNTRYID AND PLACE COUNTRYNAME THERE
                custCountryID = IDSelectionLoop("country.countryId" , "country");
                
                insertAddress = "INSERT INTO address (address.addressId, address, address2, address.cityId, postalCode, phone, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custAddressID + ", "
                                    + "'" + custAddress + "', "
                                    + "'" + custAddress2 + "', "
                                    + "" + custCityID + ", "
                                    + "'" + custPostalCode + "', "
                                    + "'" + custPhone + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
                insertCity = "INSERT INTO city (city.cityId, city, city.countryId, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custCityID + ", "
                                    + "'" + custCity + "', "
                                    + "" + custCountryID + ", "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
            
                insertCountry = "INSERT INTO country (country.countryId, country, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custCountryID + ", "
                                    + "'" + custCountry + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
            }else if(caseCheck == 3){//MEANS COUNTRY WAS EQUAL BUT CITY WAS NOT
                
                //ADD NEW ROW WITH AN AVAILABLE CITYID AND PLACE CITYNAME THERE
                custCityID = IDSelectionLoop("cityId" , "city");
                //SET CITY.COUNTRYID TO THE ONE EQUAL TO THE COUNTRYNAME
                custCountryID = countryIDFromLoop;
                
                insertAddress = "INSERT INTO address (address.addressId, address, address2, address.cityId, postalCode, phone, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custAddressID + ", "
                                    + "'" + custAddress + "', "
                                    + "'" + custAddress2 + "', "
                                    + "" + custCityID + ", "
                                    + "'" + custPostalCode + "', "
                                    + "'" + custPhone + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
                insertCity = "INSERT INTO city (city.cityId, city, city.countryId, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custCityID + ", "
                                    + "'" + custCity + "', "
                                    + "" + custCountryID + ", "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
            }else if(caseCheck == 4){//MEANS NONE OF THEM WERE EQUAL
                
                //ADD NEW ROW WITH AN AVAILABLE CITYID AND PLACE CITYNAME THERE
                custCityID = IDSelectionLoop("cityId" , "city");
                //ADD NEW ROW WITH AN AVAILABLE COUNTRYID AND PLACE COUNTRYNAME THERE
                custCountryID = IDSelectionLoop("country.countryId" , "country");
                
                insertAddress = "INSERT INTO address (address.addressId, address, address2, address.cityId, postalCode, phone, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custAddressID + ", "
                                    + "'" + custAddress + "', "
                                    + "'" + custAddress2 + "', "
                                    + "" + custCityID + ", "
                                    + "'" + custPostalCode + "', "
                                    + "'" + custPhone + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
                insertCity = "INSERT INTO city (city.cityId, city, city.countryId, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custCityID + ", "
                                    + "'" + custCity + "', "
                                    + "" + custCountryID + ", "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
            
                insertCountry = "INSERT INTO country (country.countryId, country, createDate, createdBy, lastUpdate, lastUpdateBy)\n"
                                    + "VALUES (" + custCountryID + ", "
                                    + "'" + custCountry + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "', "
                                    + "'" + custCreateDate + "', "
                                    + "'" + userName + "');\n";
                
            }else{
                System.out.println("CASECHECK ERROR! IT DID NOT HAVE A VALUE FROM 1-4!");
            }
            
            try {

                stmt = conn.createStatement();
                /*EXAMPLE CODE FOR SQL
                rs = stmt.executeQuery("SELECT city, country, start FROM city, country, appointment WHERE city.countryID = country.countryID");
                */
                
                stmt.executeUpdate(insertCustomer);
                stmt.executeUpdate(insertAddress);
                
                if(insertCity.equals("") == false && insertCountry.equals("") == false){
                    
                    stmt.executeUpdate(insertCity);
                    stmt.executeUpdate(insertCountry);
                    
                }else if(insertCity.equals("") == false && insertCountry.equals("")){
                     stmt.executeUpdate(insertCity);
                     
                }else if(insertCity.equals("") && insertCountry.equals("") == false){
                     stmt.executeUpdate(insertCountry);
                }else{
                    System.out.println("city and country queries are null");
                }
           
                /*while (rs.next()) {
                    System.out.println(rs.getString(1));
                }*/
            } catch (SQLException ex) {
                ex.printStackTrace();
            }

        } catch (ClassNotFoundException | SQLException ex) {
            ex.printStackTrace();
        }
    }
 ```

Copyright 2019 © [niknik27](https://github.com/niknik27)
