import React, { useState } from 'react';

const FileUploadForm = () => {
  const [file1, setFile1] = useState(null);
  const [file2, setFile2] = useState(null);

  const handleFile1Change = (event) => {
    setFile1(event.target.files[0]);
  };

  const handleFile2Change = (event) => {
    setFile2(event.target.files[0]);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    const formData = new FormData();
    formData.append('file1', file1);
    formData.append('file2', file2);

    // TODO: Send the formData to the Spring Boot backend
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="file" name="file1" onChange={handleFile1Change} />
      <input type="file" name="file2" onChange={handleFile2Change} />
      <button type="submit">Convert</button>
    </form>
  );
};

export default FileUploadForm;







=============





import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartFile;

@RestController
public class FileUploadController {

    @PostMapping("/upload")
    public ResponseEntity<String> uploadFiles(
            @RequestParam("file1") MultipartFile file1,
            @RequestParam("file2") MultipartFile file2) {
        try {
            // Specify the directory where you want to store the files
            String uploadDirectory = "/path/to/your/directory/";

            // Save the files to the specified directory
            file1.transferTo(new File(uploadDirectory + file1.getOriginalFilename()));
            file2.transferTo(new File(uploadDirectory + file2.getOriginalFilename()));

            // Run your desired API using the file paths
            // TODO: Implement your logic here
            
            return ResponseEntity.ok("Files uploaded successfully!");
        } catch (Exception e) {
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Error uploading files.");
        }
    }
}

