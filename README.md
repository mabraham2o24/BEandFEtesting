# Backend and Frontend Testing 
# Tools Used
### ***Front-End Testing***
### 1. JEST
    - Used for running front-end testing files
    - Executes tests, checks expected results, showing whether its a pass or fail 
### 2. JSDOM 
    - Simulates browser environment 
    - Pretends to be a browser by providing document, window, buttons, inputs, etc. 

### 3. Fetch Mocking (global.fetch) 
    - fake API calls from front-end 
    - Does not use real network calls and returns fake JSON responses so we can run the tests faster and safely. 


### ***Back-End Testing***
### 1. Jest(Bac-End Mode)
    - Runs back-end/unit/API tests 
    - Test runner that executes back-end test files and checks the results 
### 2. Supertest
    - Tests Express API endpoints 
    - Sends fake HTTP requests(GET, POST, DELETE) to the Express Server
### 3. MongoDB
    - Stores data during the tests
    - This is the actual database that is used to insert, retrieve and deleting test data
### 4. Mongoose
    - DB interactions in tests
    - Lets tests create documents(example are the weather records) and query them
### 5. dotenv 
    - Loads environment variables
    - Reads .env file so the datavse URI and API keys work properly during testing
### 6. Weather Service Mocking 
    - Fake external API calls 
    - Fakes responses from OpenWeather API so we do not hit real servers
### 7. Express 
    - In-memory test server
    - Creates a tiny Express app so Supertest can call API routes without having to start the local3000 server. 
-----
# Screenshots of Outputs and Successful Testing 
### ***All Tests PASSED***
<img width="333" height="132" alt="image" src="https://github.com/user-attachments/assets/d5664385-b358-441b-a9ed-9578a6506904" />

### ***Front-End Tests PASSING***
<img width="511" height="123" alt="image" src="https://github.com/user-attachments/assets/901911b2-2c6d-474a-a174-808c9fa62862" />

### ***Back-End API Tests PASSING***
<img width="511" height="126" alt="image" src="https://github.com/user-attachments/assets/ffad9319-6c59-44ba-8c3b-50707496f7d4" />

### ***FetchJSON Utility Tests PASSING***
<img width="524" height="130" alt="image" src="https://github.com/user-attachments/assets/66e3869f-b8f1-492b-abcb-668b665085ba" />

### ***MongoDB Connection During Testing***
<img width="1117" height="354" alt="image" src="https://github.com/user-attachments/assets/eef62ee0-6c63-45e0-a856-75c300d70328" />

### ***Code Coverage***
<img width="554" height="297" alt="image" src="https://github.com/user-attachments/assets/941ce7a0-f723-44af-b6f6-89b9c9e210fd" />

-------
# Code Screenshots & Explanations 

### ***Backend Testing***
### 1. Empty History
### This tests what happens when the databse has no weather records. It sends a GET request and expects an empty array so we know the API handles "no data" scenarios correctly. In other words ensures that the API will not crash when the databse is empty. 
<img width="1528" height="596" alt="emptyhistory" src="https://github.com/user-attachments/assets/4584e35c-c90d-4ab4-a2bb-95850239d75a" />

### 2. Get all saved documents
### This tests inserts two weather records into the databse and then calls the GET route. It ensures the API actually retrieves the data we have stored. This is testing whether or not rthe backend is correctly talking to MongoDB. 
<img width="1510" height="786" alt="getallsaveddocuments" src="https://github.com/user-attachments/assets/428c644e-1759-4398-afa3-3f496a8a8e91" />

### 3. Limit query paramter
### This is testing to see if giving a limit query restricts how many records the API returns. It confirms the API properly reads and uses query paramaters/ This is useful so when we are pulling records we do not get a huge output back and make it look cleaner. 
<img width="1464" height="672" alt="limitqueryparameter" src="https://github.com/user-attachments/assets/c5e382b8-6284-4872-afd4-ef7b86b61a63" />

### 4. Non-numeric still works 
### The tests whether the API can handle an invalid limit query(ex. ?limit=mno) and does not break. This test confirms that the API ignores the bad limit and still returns correct results. 
<img width="1542" height="672" alt="non-numericlimit" src="https://github.com/user-attachments/assets/fa05cc75-b48f-4cc6-8c2d-1a12bd5da982" />

### 5. Schema of items 
### This tests that each returned weather record contains required fields such as city, country, temperature, and humidity. This makes sure that the JSON structure is valid which is vital for the frontend. 
<img width="1402" height="862" alt="schema" src="https://github.com/user-attachments/assets/ba1a846c-9192-45da-bd2a-cefbdc80693b" />

### 6. Get one by ID
### This test saves one record and then fetches it using its MongoDB ID. This verifies whether or not the API correctly finds and returns a single record. In other words this ensures that the /api/weather/:id is working properly. 
<img width="1496" height="596" alt="getonebyID" src="https://github.com/user-attachments/assets/728a7f66-b684-4b49-bf21-ecaa5769df61" />

### 7. Get with valid but missing ID
### This test is to make sure the API does not crash when the ID format is valid but the record does not exisit in the database. It confirms the route responds with either a 404 or a safe fallback. 
<img width="1774" height="596" alt="validbutmissingid" src="https://github.com/user-attachments/assets/07350090-1c16-4a52-9241-33b601a0af08" />

### 8. Get with invalid ID format
### This test is to make sure the backend does not crash with an invalid ID. When someone sends an invalid ID, MongoDB throws and error. This test is to ensure that our program handles these type of scenarios properly and returs an error status code. 
<img width="1558" height="558" alt="invalidIDformat" src="https://github.com/user-attachments/assets/700d738b-adb4-40da-b8ac-134763d58544" />

### 9. Delete exisiting record 
### This test ensures that the delete route is actually performing properly and modifying the database. We create a weather entry, delete it, and confirm it no longer exists. This test proves that deletion is functioning end-to-end. 
<img width="1480" height="710" alt="deleteexistingrecord" src="https://github.com/user-attachments/assets/8d9a35cc-0bb8-4ec3-a1b7-0a25c4bb9876" />

### 10. Delete on the targeted record
### Create two records and delete only one of them. This test ensures that the delete route is not removing more records than we want to. 
<img width="1556" height="748" alt="deletetargetedrecord" src="https://github.com/user-attachments/assets/b57624fd-e7a4-471b-b3de-78816ee8a96c" />

### 11. Delete with invalid ID format
### If the user inputs an invalid ID the backend should NOT crash. This test checks that the API returns an error status safely. In other words this is testing whether or not the route can handle invalid inputs. 
<img width="1558" height="482" alt="deleteinvalidID" src="https://github.com/user-attachments/assets/09356312-7f1e-452a-8205-4ad46de82956" />

### 12. Delete with valid but missing ID
### This test deletes a record using a valid ID that does not exists. It verifies the server responds with an error(commonly a 404 error). 
<img width="1666" height="596" alt="deletevalidbutmissingID" src="https://github.com/user-attachments/assets/b3d949dc-ec32-49aa-8b66-8d3f18fc7bde" />

### 13. After delete, GET should fail 
### We delete a record and then attempt to use the GET operation to retrieve the same record. The GET should fail which proves the record was successfully deleted. 
<img width="1712" height="634" alt="afterdeleteGET" src="https://github.com/user-attachments/assets/3d806539-8a9f-487f-b938-b364f67a9a54" />

### 14. Multiple records + ordering 
### Inserts two records with different timestamps. It ensures the API returns both records in order(only if we have a sorting funtion implemented). 
<img width="1834" height="938" alt="multiplerecordsandordering" src="https://github.com/user-attachments/assets/969c6cc9-f63c-498d-b70e-178de9df70cc" />

### 15. Numeric temperature and humidity edge case
### This test is to make sure the system does not break if temperature and humidity is set at "0". This ensures the backend stores and returns numeric data correctly. 
<img width="1418" height="710" alt="numerictempandhumidity" src="https://github.com/user-attachments/assets/ae97ab2b-344b-4e9b-b2c2-1d9d4e1f7c63" />

### 16. Coordinates store properly 
### This test ensures that the coordinates remains intact. It makes sure that latitude and longitude are stored and returned as a nested object. 
<img width="1326" height="824" alt="coordinatesstoredproperly" src="https://github.com/user-attachments/assets/51d9da36-a879-4d57-8e85-ba56994c34fc" />

### 17. Description and condition strings 
### This test is to ensure that the data type is consistent. It tests whether or not the weather summary fields are returned in proper string format. This is vital because this is what the frontend pulls to display. 
<img width="1588" height="900" alt="descriptionandconditionstrings" src="https://github.com/user-attachments/assets/b865ed3a-3617-404d-85b0-9fd71cc92154" />

### 18. Large History
### This test is to ensure that the API does not crash if huge amounts of data is inserted. 
<img width="1388" height="748" alt="largehistory" src="https://github.com/user-attachments/assets/2fc430fd-3595-4bfe-babb-3a71b54947ff" />

### 19. Real city fetch 
### Testing the fetch route using a real city so it can be ensured that the external API call works and the route is functional. 
<img width="1542" height="634" alt="realcityfetch" src="https://github.com/user-attachments/assets/b2da9a6e-18df-47ee-ad59-46846529e749" />

### 20. Fake city fetch error 
### This test is to ensure the API can handle invalid city inputs(fake city names). It should not crash but instead throw a simple error message. 
<img width="1756" height="710" alt="fakecityfetch" src="https://github.com/user-attachments/assets/cfc08950-5ea5-406b-bdc5-1d145f0cb369" />

------
### ***Frontend Testing***

### 1.setStatus - normal message
### This test confirms that setStatus("History loaded.", "ok") updates the text and addes ok CSS class. This ensures the function correctly updates the UI to show the successful message. 
<img width="1388" height="596" alt="setStatus" src="https://github.com/user-attachments/assets/f8862683-5b5d-4b32-97a6-2ba9d2f08bcc" />

### 2.setStatus - error message
### This test is to ensure that when something goes wrong an error message is thrown to notify the user. It tests how the UI responds to a sample failure situation. 
<img width="1434" height="596" alt="setstatusError" src="https://github.com/user-attachments/assets/eac7389c-4b95-4ff0-87d1-cb235a6bd6ab" />

### 3.renderLatest - normal data
### This tests whether the UI displays the latest weather card correctly and lists the correct city and values by inserting a fake record. 
<img width="1294" height="1052" alt="renderLatestnormaldata" src="https://github.com/user-attachments/assets/c9805b33-8fd2-4520-8477-c57b64088ab2" />

### 4.renderLatest - missing temperature
### This is testing that the UI returns N/A for any missing values from the returned API data rather than the UI comnpletely breaking. 
<img width="1480" height="748" alt="renderLatestmissingtemp" src="https://github.com/user-attachments/assets/252203c1-3e49-40c0-af10-fb2032267ac1" />

### 5.renderHistory - no data
### This tests whether or not the UI shows a simple message informing the user there is no data rather than returning an empty table. 
<img width="1480" height="634" alt="renderHistory" src="https://github.com/user-attachments/assets/8b3a5cf6-c11e-4c8c-859f-4c794c08ac09" />

### 6.renderHistory - rows per record
### Tests whether or not the UI properly parses through the data and displays it correctly in consistency with the backend. For example if two records are inserted there should be TWO ROWS. 
<img width="1264" height="1280" alt="renderHistoryrowsperrecord" src="https://github.com/user-attachments/assets/7b6a9636-e15a-4815-a64a-38fc307461d9" />

### 7.renderHistory - button in each row
### This tests that the interactive parts of the UI are created correctly and each row consists of a refresh and delete button properly. 
<img width="1448" height="1128" alt="renderHistorybuttons" src="https://github.com/user-attachments/assets/c521be71-90ed-42b2-8404-297f2af173fb" />

### 8.handleSearch - success path 
### Test to ensure the search works properly in normal scenarios. The test simulates a user entering a city, mock the fetch API and checks the success message. 
<img width="1572" height="1660" alt="handleSearchsuccess" src="https://github.com/user-attachments/assets/85222e2f-7e25-4b55-a1b2-eb52da33babc" />

### 9.handleSearch - error path
### This tests that when something goes wrong with the API the UI does not fully crash but just display an error message. 
<img width="1556" height="1052" alt="handleSearcherror" src="https://github.com/user-attachments/assets/1f371ca2-63a5-45af-a79d-44c37adfd143" />

### 10.deleteWeather - user cancels 
### This test ensures that if the user cancels their request nothing gets sent and everything stays the same. 
<img width="1634" height="672" alt="deleteWeather" src="https://github.com/user-attachments/assets/5a80a38f-68fc-45f1-9a53-adc2d74a9716" />

-----
### ***Small Utility Tests***
### 1.fetchJSON - success
### This test mocks the browser fetch function to succeed. It ensures that or wrapper function returns the JSON correctly. 
<img width="1202" height="824" alt="fetchJSONsuccess" src="https://github.com/user-attachments/assets/c6a9f76d-9f44-448c-ae12-17ddfa15f5a9" />

### 2.fetchJSON - error
### This test mocks fetch to return an error response. It confirms whether or not the UI can show meaningful error messages. 
<img width="1356" height="672" alt="fetchJSONerror" src="https://github.com/user-attachments/assets/a523ef40-3275-4aa3-be36-e9cbba449c99" />







