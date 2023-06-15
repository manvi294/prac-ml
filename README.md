import axios from 'axios';

const submitFiles = async () => {
  const formData = new FormData();
  for (let i = 0; i < files.length; i++) {
    formData.append("files", files[i]);
  }

  try {
    const response = await axios.post("http://localhost:8080/api/upload", formData);

    // Handle the response from the backend
    // ...
  } catch (error) {
    // Handle errors
    // ...
  }
};
