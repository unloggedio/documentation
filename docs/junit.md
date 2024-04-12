# Generating JUnit Tests with Unlogged

With Unlogged.io, you have the capability to convert recordings of code execution into JUnit tests. This innovative feature is designed to streamline the testing process, making it more efficient and effective.

## How Does It Work?
Unlogged.io tracks the execution of your code as it runs. This tracking captures all the necessary details of the code’s behavior and outputs. Following the completion of code execution, Unlogged utilizes this recording to generate JUnit tests. 

**These tests reflect the recorded execution path and outcomes, emulating real world scenarios.**

![](assets/images/junit.gif)

!!! tip Utilizing Boilerplate Generation
    If generating JUnit tests post-execution does not align with your workflow, or if you prefer to set up tests in advance, Unlogged.io offers a boilerplate generation option. This feature allows you to create template-based tests before running your actual code. 


The `canDeliverToCustomer` method below determines if a delivery can be made to a customer based on their location and weather conditions:

1. **Fetch Customer Profile**: Retrieves customer information using their ID.
2. **Extract Location**: Converts the customer's address into a location format.
3. **Weather Check**: Retrieves the weather for the customer's location.
4. **Check Delivery Unit Availability**: Determines if any delivery units are available at the location.
5. **Delivery Decision**:
   - If no units are available, returns that delivery is not possible.
   - Checks weather conditions (specifically precipitation) to decide if delivery is feasible.
6. **Report Generation**: Writes a report based on the feasibility of delivery and returns the result with the customer profile and weather information.

``` java
    public DeliveryCheckResponse canDeliverToCustomer(long customerId) {
        CustomerProfile customerProfile = customerProfileRepo.getByCustomerId(customerId);
        String location = LocationUtils.getLocationFromAddress(customerProfile.getAddress());
        WeatherInfo weatherInfo = weatherService.getWeatherForAddress(location);

        List<DeliveryUnit> availableUnits = deliveryUnitService.getAvailableUnitsForLocation(
                deliveryUnitService.getAllDeliveryUnits(), location);
        if (availableUnits.size() == 0) {
            return new DeliveryCheckResponse(customerProfile, false, false, weatherInfo);
        }

        boolean canDeliver = false;
        if (weatherInfo.getCurrent().getPrecip_mm() < 2.51) {
            canDeliver = true;
        }
        boolean reportWritten = localFileService.writeReport(canDeliver, customerProfile);
        return new DeliveryCheckResponse(customerProfile,
                reportWritten, reportWritten && canDeliver, weatherInfo);
    } 
```

Here is the JUnit Test generated for the code above:

```java
   public final class TestDeliveryServiceV {

    private DeliveryService deliveryService;
    private CustomerProfileRepo customerProfileRepo;
    private WeatherService weatherService;
    private DeliveryUnitService deliveryUnitService;
    private ObjectMapper objectMapper = new ObjectMapper();

    @BeforeEach
    public void setup() throws Exception {
        customerProfileRepo = Mockito.mock(CustomerProfileRepo.class);
        deliveryService = new DeliveryService();
        injectField(deliveryService, "customerProfileRepo", customerProfileRepo);
        weatherService = Mockito.mock(WeatherService.class);
        deliveryUnitService = Mockito.mock(DeliveryUnitService.class);
        injectField(deliveryService, "weatherService", weatherService);
        injectField(deliveryService, "deliveryUnitService", deliveryUnitService);
    }

    @Test
    public void testCanDeliverToCustomer() throws Exception {
        CustomerProfile byCustomerId = objectMapper.readValue("{\"customerid\":4,\"customername\":\"ohn Doe\",\"dateofbirth\":\"70-10-20\",\"email\":\"JD@mail\",\"contactnumber\":\"999-999\",\"address\":\"304 Alainis Parkway, Boylemouth, Virginia\",\"referralcodes\":[\"JGSDFS, FEFWEF, FWEFDF\"],\"createdDate\":\"Apr 12, 2024 12:54:08 PM\",\"updatedDate\":\"Apr 12, 2024 12:54:08 PM\"}", CustomerProfile.class);
        Mockito.when(customerProfileRepo.getByCustomerId(eq(4L))).thenReturn(byCustomerId);
        
        WeatherInfo weatherForAddress = objectMapper.readValue("{\"location\":{\"name\":\"Virginia Beach\",\"region\":\"Virginia\",\"country\":\"United States of America\",\"lat\":36.85,\"lon\":-75.98,\"tz_id\":\"America/New_York\",\"localtime_epoch\":1712906551,\"localtime\":\"2024-04-12 3:22\"},\"current\":{\"temp_c\":21.1,\"temp_f\":70.0,\"is_day\":0,\"condition\":{\"text\":\"Partly cloudy\",\"icon\":\"//cdn.weatherapi.com/weather/64x64/night/116.png\",\"code\":1003},\"wind_mph\":15.0,\"wind_kph\":24.1,\"wind_degree\":210,\"wind_dir\":\"SSW\",\"pressure_mb\":998.0,\"pressure_in\":29.48,\"precip_mm\":0.35,\"precip_in\":0.01,\"humidity\":84,\"cloud\":50,\"feelslike_c\":21.1,\"feelslike_f\":70.0,\"vis_km\":16.0,\"vis_miles\":9.0,\"uv\":1.0,\"gust_mph\":37.6,\"gust_kph\":60.5}}", WeatherInfo.class);
        Mockito.when(weatherService.getWeatherForAddress(eq("Virginia"))).thenReturn(weatherForAddress);

        List<DeliveryUnit> availableUnitsForLocation = objectMapper.readValue("[]", new TypeReference<List<DeliveryUnit>>() {});
        Mockito.when(deliveryUnitService.getAvailableUnitsForLocation(any(Object.class), eq("Virginia"))).thenReturn(availableUnitsForLocation);

        List<DeliveryUnit> allDeliveryUnits = objectMapper.readValue("[]", new TypeReference<List<DeliveryUnit>>() {});
        Mockito.when(deliveryUnitService.getAllDeliveryUnits()).thenReturn(allDeliveryUnits);

        DeliveryCheckResponse deliveryCheckResponse = deliveryService.canDeliverToCustomer(4L);
        DeliveryCheckResponse deliveryCheckResponseExpected = objectMapper.readValue("{\"customerProfile\":{\"customerid\":4,\"customername\":\"ohn Doe\",\"dateofbirth\":\"70-10-20\",\"email\":\"JD@mail\",\"contactnumber\":\"999-999\",\"address\":\"304 Alainis Parkway, Boylemouth, Virginia\",\"referralcodes\":[\"JGSDFS, FEFWEF, FWEFDF\"],\"createdDate\":\"Apr 12, 2024 12:54:08 PM\",\"updatedDate\":\"Apr 12, 2024 12:54:08 PM\"},\"requestWritten\":false,\"canDeliver\":false,\"weatherInfo\":{\"location\":{\"name\":\"Virginia Beach\",\"region\":\"Virginia\",\"country\":\"United States of America\",\"lat\":36.85,\"lon\":-75.98,\"tz_id\":\"America/New_York\",\"localtime_epoch\":1712906551,\"localtime\":\"2024-04-12 3:22\"},\"current\":{\"temp_c\":21.1,\"temp_f\":70.0,\"is_day\":0,\"condition\":{\"text\":\"Partly cloudy\",\"icon\":\"//cdn.weatherapi.com/weather/64x64/night/116.png\",\"code\":1003},\"wind_mph\":15.0,\"wind_kph\":24.1,\"wind_degree\":210,\"wind_dir\":\"SSW\",\"pressure_mb\":998.0,\"pressure_in\":29.48,\"precip_mm\":0.35,\"precip_in\":0.01,\"humidity\":84,\"cloud\":50,\"feelslike_c\":21.1,\"feelslike_f\":70.0,\"vis_km\":16.0,\"vis_miles\":9.0,\"uv\":1.0,\"gust_mph\":37.6,\"gust_kph\":60.5}}}", DeliveryCheckResponse.class);
        Assertions.assertEquals(deliveryCheckResponseExpected, deliveryCheckResponse);
    }
}

```

## How's this different from co-pilot and AI generated tests?

Unlogged.io stands out in the Java development tools space with several unique features. We offer runtime mocking, performance tracking, and real-time visual code coverage, which are not commonly available in similar products. 

Additionally, Unlogged offers specific capabilities for handling real-world data and scenarios, providing developers with tools to test and refine code under realistic conditions. 

| Features                          | Unlogged   | Co-Pilot  | diffblue   | sapient ai | codium AI  | IntelliJ AI |
|-----------------------------------|------------|-----------|------------|------------|------------|-------------|
| Runtime mocking                   | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| Bulk JUnit Test Generation        | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> |
| Performance Tracking              | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| No Code Tests                     | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> |
| Code Generation using AI          | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |
| Real World Data/Scenarios         | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| Real Time Visual Code Coverage    | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| PR Documentation                  | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |
| Convert from one Language to another | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |



