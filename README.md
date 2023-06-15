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
