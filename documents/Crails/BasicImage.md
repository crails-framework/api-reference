Implementation of the [Attachment] class from `libcrails-attachment` which provides methods that help you resize or crop images to a given sizes.

```cpp
void MyController::action()
{
  Crails::BasicImage upload, avatar;
  User user;

  // Persist the file uploaded in the user[avatar] field into storage
  upload.use_uploaded_file(params.get_upload("user[avatar]");

  try
  {
    // Create a new resized image of 200x400 pixels
    avatar = upload.resized(200, 400);

    // Save a reference to the image file 
    user.set_avatar(avatar);
    database.save(user);
  }
  catch (...)
  {
    // In case we couldn't save the model, remove the avatar from storage
    avatar.cleanup_files();
  }

  // Whatever happens, remove the original file from storage
  upload.cleanup_files();
}
```

You may also preserve the aspect ratio of the original image when resizing it using the `BasicImage::PreserveAspectRatio` option:

```cpp
Crails::BasicImage avatar = upload.resized(200, 400, Crails::BasicImage::PreserveAspectRatio);
```
