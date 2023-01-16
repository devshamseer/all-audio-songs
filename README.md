# All Songs Api

## get free unlimited songs

1. copy the link


  ```sh
  https://devshamseer.github.io/all-audio-songs/allsongs/sonng1.mp3
  ```
2. add you get api code
## Flutter using diopackage

1. Add dependency
  ```sh
  dependencies:
  dio: ^4.0.6
  ```
  2. import package

  ```sh
import 'package:dio/dio.dart';
  ```
3. Get songs count

  ```sh

import 'package:dio/dio.dart';


 var songcount;
  var songsList = [];
  getSonngCount() async {
    try {
      var response = await Dio().get(
          'https://devshamseer.github.io/all-audio-songs/allsongcount.json');
      songcount = await response.data["count"];
      print("Data${response.data["count"]}");
    } catch (e) {
      print(e);
    }
  
  }


  ```
  4. Add count from loop
  
  ```sh
import 'package:dio/dio.dart';
  getSongList() async {
    await getSonngCount();
    for (var i = 1; i <= songcount; i++) {
      var songs =
          "https://devshamseer.github.io/all-audio-songs/allsongs/sonng${i}.mp3";
      songsList.add(songs);

      var seen = Set<String>();
      songsList = songsList.where((songs) => seen.add(songs)).toList();
    }

  
  }
  ```
  
