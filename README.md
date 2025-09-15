
# freesound-juce


A JUCE client for accessing the [Freesound](https://freesound.org) API. From the Freesound API docs:

> With the Freesound API you can browse, search, and retrieve information about Freesound users, packs, and the sounds themselves of course. You can find similar sounds to a given target (based on content analysis) and retrieve automatically extracted features from audio files, as well as perform advanced queries combining content analysis features and other metadata (tags, etc…). With the Freesound API, you can also upload, comment, rate and bookmark sounds!

The freesound-juce client automatically maps function arguments to HTTP parameters of the Freesound API. JSON results are parsed and converted to C++ objects. The main object classes (`SoundList`, `Sound`,
`User`, `Pack`) implement utility methods to further interact with the API.

The freesound-juce client includes a simple example command line application built with JUCE v5.4.4 which shows how to use it. Client's [documentation can be found here](https://mtg.github.io/freesound-juce/index.html). However we recommend you to check the [official Freesound API documentation]((https://freesound.org/docs/api/)) to get more information about the available API endpoints and features.


## Usage

This repository is a CMake project that uses JUCE as a submodule. To build it, you need to have CMake. 

There is no need to manually download JUCE, as it is included as a git submodule. To clone the repository with the JUCE submodule, use:

## Compatibility

For now, we have only tested the latest version of the API on MacOS. We will provide windows and linux support soon as well. 


### Freesound API Key

To build the project from CMake, you need to provide your Freesound API key and client id as CMake variables.

You can request an API key at [http://freesound.org/apiv2/apply/](http://freesound.org/apiv2/apply/).

Once you have your API key and client id, you can provide them to CMake as follows:

```commandline
    -DFREESOUND_API_KEY=your_api_key -DFREESOUND_CLIENT_ID=your_client_id
```


## Quick example

```cpp
FreesoundClient client(secret);
SoundList list = client.textSearch("bass");
Array<FSSound> arrayOfSearch = list.toArrayOfSounds();
for (int i = 0; i < arrayOfSearch.size(); i++) {
  name = arrayOfSearch[i].name;
  username = arrayOfSearch[i].user;
  std::cout << "Sound Name: " << name << " Username: " << username << std::endl;
}

```


## Example applications

Check out this cool example apps:

* [Demo app](https://github.com/aframires/freesound-juce/blob/master/Source/Main.cpp): simple command-line utility that makes some queries to Freesound to demonstrate how the client works. Includes OAuth2 authentication example as well.
* [FreesoundUploader](https://github.com/aframires/FreesoundUploader): let's you upload sounds to Freesound directly from your DAW!
* [FreesoundSimpleSampler](https://github.com/ffont/FreesoundSimpleSampler): let's you search in Freesound and automatically build a simple sampler based on the results.




### NOTE

The original source code from a few years ago is available at [https://github.com/mtg/freesound-juce](https://github.com/mtg/freesound-juce).

After full adaptation to the latest Freesound API and JUCE versions, the code will be moved back to the original repository.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.