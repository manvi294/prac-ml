import java.io.File;

public class FileTypeChecker {

    public static void main(String[] args) {
        String folderPath = "path/to/your/folder"; // Specify the path to your folder here

        File folder = new File(folderPath);

        if (folder.isDirectory()) {
            File[] files = folder.listFiles();

            if (files != null) {
                for (File file : files) {
                    if (file.isFile()) {
                        String fileName = file.getName();
                        String extension = getFileExtension(fileName);

                        if (extension.equalsIgnoreCase("txt")) {
                            // Handle .txt file
                            System.out.println("Text file found: " + fileName);
                        } else if (extension.equalsIgnoreCase("json")) {
                            // Handle .json file
                            System.out.println("JSON file found: " + fileName);
                        }
                    }
                }
            }
        }
    }

    private static String getFileExtension(String fileName) {
        int dotIndex = fileName.lastIndexOf('.');
        if (dotIndex > 0 && dotIndex < fileName.length() - 1) {
            return fileName.substring(dotIndex + 1).toLowerCase();
        }
        return "";
    }
}
