import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

@RestController
public class FileController {

    @PostMapping("/api/sendFiles")
    public Map<String, String> sendFiles(@RequestBody Map<String, Boolean> requestBody) {
        boolean booleanValue = requestBody.getOrDefault("booleanValue", false);

        // Generate the files
        File file1 = generateFile("file1.txt", "This is file 1");
        File file2 = generateFile("file2.txt", "This is file 2");

        // Assuming you have the URLs of the generated files
        String file1Url = getFileUrl(file1);
        String file2Url = getFileUrl(file2);

        // Create a response with the file URLs
        Map<String, String> response = new HashMap<>();
        response.put("file1Url", file1Url);
        response.put("file2Url", file2Url);
        return response;
    }

    private File generateFile(String fileName, String content) {
        try {
            File file = new File(fileName);
            FileWriter writer = new FileWriter(file);
            writer.write(content);
            writer.close();
            return file;
        } catch (IOException e) {
            e.printStackTrace();
            // Handle the exception appropriately
            return null;
        }
    }

    private String getFileUrl(File file) {
        // Generate the URL for the file and return it
        // This could be a public URL or an endpoint in your backend to serve the file
        // For simplicity, let's assume we have a file serving endpoint in the same API
        return "/api/files/" + file.getName();
    }
}