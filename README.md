THESE ARE STILL A WORK IN PROGRESS (except the non Framework Specific Layer Symfony 3 implementation).<br /><br />
DOCUMENTATION IS NEEDED FOR MOST OF THE PROJECTS.<br /><br />
THE V3s3 API DOES NOT REQUIRE A HTTP "Accept" HEADER TO BE SENT WITH GET (READ) REQUESTS. INSTEAD IT STORES THE "Content-Type" HTTP REQUEST HEADER VALUE AS PART OF THE STORED OBJECT IN THE DATABASE ON A PUT (CREATE) REQUEST OR IF THE HEADER IS MISSING THE CONTENT TYPE IS DETERMINED FROM THE OBJECT'S DATA USING PHP'S FILEINFO MODULE.<br /><br />

# The V3s3 API
This API has three standard actions - Create, Read and Delete corresponding to the PUT, GET and DELETE HTTP methods (yes PUT is used to create an object).<br />
There is also a non-standard POST request for pulling structured summary data for multiple objects.
