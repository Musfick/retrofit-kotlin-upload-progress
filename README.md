Retrofit Request Body With Progress(Kotlin)
========================

## Introduction
This library allows you to get upload progress from [Retrofit][1] Request Body

Support
-----
✅ Single File Upload <br/>
✅ Multiple File Upload

Usage
-----

This library allows you to specify your service interface as:
```kotlin
interface Service {
    @POST("/posts")
    fun createPost(@Body body: RequestBody): Response<Post>
}
```

And then in your repository:
```kotlin
val bodyBuilder = MultipartBody.Builder().setType(MultipartBody.FORM)

bodyBuilder.addFormDataPart("title", "Post Title")
bodyBuilder.addFormDataPart("description", "Post Description")

//File
bodyBuilder.addFormDataPart("image", file.name, file.asRequestBody("image/*".toMediaTypeOrNull()))
bodyBuilder.addFormDataPart("video", file.name, file.asRequestBody("video/*".toMediaTypeOrNull()))

val requestBody = bodyBuilder.build()
val requestBodyWithProgress = ReqBodyWithProgress(requestBody){progress ->
    //If you use logging interceptor this will trigger twice
    Log.d("Upload Progress:",""+progress)
}

val call = service.createPost(requestBodyWithProgress)
```

## Setup

Currently available via [JitPack][2].

To use it, add the jitpack maven repository to your `build.gradle` file:
```gradle
repositories {
  ...
  maven { url "https://jitpack.io" }
  ...
}
```
and add the dependency:
```gradle
dependencies {
  ...
  implementation 'com.github.Musfick:retrofit-kotlin-upload-progress:0.1.0'
  ...
}
```

## License

    Copyright 2021 Musfick Jamil

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[1]: http://square.github.io/retrofit/
[2]: https://jitpack.io
