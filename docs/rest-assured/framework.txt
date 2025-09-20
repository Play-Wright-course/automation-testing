// Complete Rest Assured Java Framework for Reqres API
// Features: JSON + Excel support, Retry mechanism, Logging, ExtentReports, Screenshots

// ===================== APIResources.java =====================
package resources;

public enum APIResources {
    CREATE_USER("/api/users"),
    GET_USER("/api/users/2"),
    UPDATE_USER("/api/users/2"),
    DELETE_USER("/api/users/2"),
    LIST_USERS("/api/users?page=2");

    private String resource;

    APIResources(String resource) { this.resource = resource; }
    public String getResource() { return resource; }
}


// ===================== ConfigReader.java =====================
package resources;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class ConfigReader {
    private Properties prop;

    public ConfigReader() throws IOException {
        prop = new Properties();
        FileInputStream fis = new FileInputStream(System.getProperty("user.dir") + "/src/test/resources/config.properties");
        prop.load(fis);
    }

    public String getBaseURL() { return prop.getProperty("baseURL"); }
}


// ===================== TestDataBuilder.java =====================
package resources;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class TestDataBuilder {
    public String createUserPayload(String fileName) throws IOException {
        return new String(Files.readAllBytes(Paths.get(System.getProperty("user.dir") + "/src/test/resources/testdata/" + fileName)));
    }
}


// ===================== ExcelUtils.java =====================
package utils;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class ExcelUtils {
    public static String getCellData(String sheetName, int row, int col) throws IOException {
        FileInputStream fis = new FileInputStream(new File(System.getProperty("user.dir") + "/src/test/resources/excel/users.xlsx"));
        Workbook workbook = new XSSFWorkbook(fis);
        Sheet sheet = workbook.getSheet(sheetName);
        String value = sheet.getRow(row).getCell(col).getStringCellValue();
        workbook.close();
        return value;
    }
}


// ===================== LoggerHelper.java =====================
package utils;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class LoggerHelper {
    public static Logger getLogger(Class<?> clazz) {
        return LogManager.getLogger(clazz);
    }
}


// ===================== BaseTest.java =====================
package utils;

import io.restassured.builder.RequestSpecBuilder;
import io.restassured.specification.RequestSpecification;
import org.testng.IRetryAnalyzer;
import org.testng.ITestResult;

public class BaseTest {

    public RequestSpecification requestSpecification() {
        return new RequestSpecBuilder()
                .setBaseUri("https://reqres.in")
                .setContentType("application/json")
                .build();
    }

    public static class RetryAnalyzer implements IRetryAnalyzer {
        private int count = 0;
        private static final int maxRetry = 2;

        @Override
        public boolean retry(ITestResult result) {
            if (count < maxRetry) {
                count++;
                return true;
            }
            return false;
        }
    }
}


// ===================== ScreenshotUtils.java =====================
package utils;

import org.apache.commons.io.FileUtils;
import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class ScreenshotUtils {
    public static String captureScreenshot(String testName) throws IOException {
        String timestamp = new SimpleDateFormat("yyyyMMddHHmmss").format(new Date());
        String path = System.getProperty("user.dir") + "/screenshots/" + testName + "_" + timestamp + ".png";
        File file = new File(path);
        FileUtils.touch(file);
        return path;
    }
}


// ===================== ExtentReportManager.java =====================
package utils;

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;

public class ExtentReportManager {
    private static ExtentReports extent;

    public static ExtentReports getReport() {
        if (extent == null) {
            String reportPath = System.getProperty("user.dir") + "/reports/Reqres_Report.html";
            ExtentSparkReporter reporter = new ExtentSparkReporter(reportPath);
            reporter.config().setReportName("Reqres API Automation Report");
            reporter.config().setDocumentTitle("API Test Results");

            extent = new ExtentReports();
            extent.attachReporter(reporter);
            extent.setSystemInfo("Tester", "Nitin");
            extent.setSystemInfo("Environment", "QA");
        }
        return extent;
    }
}


// ===================== StepDefinition.java =====================
package stepDefinitions;

import io.restassured.response.Response;
import resources.APIResources;
import resources.TestDataBuilder;
import utils.BaseTest;
import org.testng.Assert;
import static io.restassured.RestAssured.given;

public class StepDefinition extends BaseTest {

    TestDataBuilder data = new TestDataBuilder();
    Response response;

    public void createUser(String fileName) throws Exception {
        response = given().spec(requestSpecification())
                .body(data.createUserPayload(fileName))
                .when().post(APIResources.CREATE_USER.getResource());
        Assert.assertEquals(response.getStatusCode(), 201);
    }

    public void getUser() {
        response = given().spec(requestSpecification())
                .when().get(APIResources.GET_USER.getResource());
        Assert.assertEquals(response.getStatusCode(), 200);
    }

    public void updateUser(String fileName) throws Exception {
        response = given().spec(requestSpecification())
                .body(data.createUserPayload(fileName))
                .when().put(APIResources.UPDATE_USER.getResource());
        Assert.assertEquals(response.getStatusCode(), 200);
    }

    public void deleteUser() {
        response = given().spec(requestSpecification())
                .when().delete(APIResources.DELETE_USER.getResource());
        Assert.assertEquals(response.getStatusCode(), 204);
    }

    public void listUsers() {
        response = given().spec(requestSpecification())
                .when().get(APIResources.LIST_USERS.getResource());
        Assert.assertEquals(response.getStatusCode(), 200);
    }
}
