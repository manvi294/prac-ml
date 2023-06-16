@RestController
@RequestMapping("/api")
public class FileController {

    @GetMapping("/download")
    public ResponseEntity<Resource> downloadFile() {
        String filePath = "/path/to/your/file"; // Replace with your actual file path

        // Load file as Resource
        Resource resource = new FileSystemResource(filePath);

        // Check if file exists
        if (!resource.exists()) {
            return ResponseEntity.notFound().build();
        }

        // Set the appropriate content type for the file
        String contentType = "application/octet-stream"; // You can set specific content types based on file extensions if needed

        // Return the file as a ResponseEntity, which will trigger a download on the frontend
        return ResponseEntity.ok()
                .contentType(MediaType.parseMediaType(contentType))
                .header(HttpHeaders.CONTENT_DISPOSITION, "attachment; filename=\"" + resource.getFilename() + "\"")
                .body(resource);
    }
}



©©©©©©©©©©


function handleDownload() {
  fetch('http://localhost:8080/api/download')
    .then(response => {
      // Check if the response was successful
      if (!response.ok) {
        throw new Error('File download failed');
      }

      // Extract the filename from the Content-Disposition header
      const contentDispositionHeader = response.headers.get('content-disposition');
      const filenameMatch = contentDispositionHeader.match(/filename="(.+)"/);
      const filename = filenameMatch && filenameMatch[1];

      // Create a blob URL from the response body
      return response.blob().then(blob => {
        const url = window.URL.createObjectURL(blob);

        // Create a temporary link element and trigger the download
        const link = document.createElement('a');
        link.href = url;
        link.download = filename || 'downloaded_file';
        link.click();

        // Clean up the blob URL
        URL.revokeObjectURL(url);
      });
    })
    .catch(error => {
      console.error('Error downloading file:', error);
    });
}
