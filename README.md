import org.springframework.core.io.FileSystemResource;
import org.springframework.core.io.Resource;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.util.LinkedMultiValueMap;
import org.springframework.util.MultiValueMap;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
@RequestMapping("/api")
public class FileController {

    @GetMapping("/download-files")
    public ResponseEntity<MultiValueMap<String, Resource>> downloadFiles() {
        String jsonFilePath = "path/to/your/json/file.json"; // Replace with the actual JSON file path
        Resource jsonResource = new FileSystemResource(jsonFilePath);

        String textFilePath = "path/to/your/text/file.txt"; // Replace with the actual text file path
        Resource textResource = new FileSystemResource(textFilePath);

        MultiValueMap<String, Resource> resources = new LinkedMultiValueMap<>();
        resources.put("jsonFile", Arrays.asList(jsonResource));
        resources.put("textFile", Arrays.asList(textResource));

        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.MULTIPART_FORM_DATA);

        return new ResponseEntity<>(resources, headers, HttpStatus.OK);
    }
}
