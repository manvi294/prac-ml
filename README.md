import org.springframework.core.io.FileSystemResource;
import org.springframework.core.io.Resource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.io.File;
import java.io.IOException;

@RestController
public class TranslatorController {

    @GetMapping("/download")
    public ResponseEntity<Resource> downloadFile() throws IOException {
        // Determine the file type based on the backend functionality (e.g., case 1: .txt, case 2: .json)
        String fileType = determineFileType(); // Your logic to determine the file type

        // Get the file path based on the file type
        String filePath = getFileForType(fileType); // Your logic to get the file path for the given file type

        // Create a file object
        File file = new File(filePath);

        // Create a Resource from the file
        Resource resource = new FileSystemResource(file);

        // Set the Content-Disposition header to force download
        HttpHeaders headers = new HttpHeaders();
        headers.add(HttpHeaders.CONTENT_DISPOSITION, "attachment; filename=" + file.getName());

        // Set the content type based on the file type
        MediaType mediaType = determineMediaType(fileType); // Your logic to determine the appropriate media type

        return ResponseEntity.ok()
                .headers(headers)
                .contentLength(file.length())
                .contentType(mediaType)
                .body(resource);
    }

    // Example method to determine the file type based on the backend functionality
    private String determineFileType() {
        // Your logic to determine the file type based on the backend functionality
        // This could be based on a flag, condition, or any other criteria
        // Return the appropriate file type (e.g., "txt" or "json")
        return "txt";
    }

    // Example method to get the file path based on the file type
    private String getFileForType(String fileType) {
        // Your logic to get the file path based on the file type
        // This could involve different paths, directories, or file names
        // Return the appropriate file path based on the file type
        if (fileType.equalsIgnoreCase("txt")) {
            return "path/to/your/textfile.txt";
        } else if (fileType.equalsIgnoreCase("json")) {
            return "path/to/your/jsonfile.json";
        } else {
            throw new IllegalArgumentException("Invalid file type");
        }
    }

    // Example method to determine the media type based on the file type
    private MediaType determineMediaType(String fileType) {
        // Your logic to determine the appropriate media type based on the file type
        // Return the appropriate media type based on the file type
        if (fileType.equalsIgnoreCase("txt")) {
            return MediaType.TEXT_PLAIN;
        } else if (fileType.equalsIgnoreCase("json")) {
            return MediaType.APPLICATION_JSON;
        } else {
            throw new IllegalArgumentException("Invalid file type");
        }
    }
}
