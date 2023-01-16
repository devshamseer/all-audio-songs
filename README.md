# All Songs Api

## get free unlimited songs
| S | H | A | M | S | E | E | R |
|-||-||-||-||-||-||-||-|

   <img src="https://images.unsplash.com/photo-1673868077539-9c3120f78420?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80" alt="Logo" width="400" height="600">

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
  5. Add the code 
  
  
  ```sh
import 'package:dio/dio.dart';
import 'package:flutter/material.dart';
import 'package:just_audio/just_audio.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Remove the debug banner
      debugShowCheckedModeBanner: false,

      home: Getsongs(),
    );
  }
}

class Getsongs extends StatefulWidget {
  const Getsongs({super.key});

  @override
  State<Getsongs> createState() => _GetsongsState();
}

class _GetsongsState extends State<Getsongs> {
  var songcount;
  var songsList = [];
  @override
  void initState() {
    // TODO: implement initState
    getSonngCount();
    getSongList();

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
          child: songsList == null || songsList == ""
              ? Center(
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.center,
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      CircularProgressIndicator(
                        color: Colors.green,
                      ),
                      SizedBox(
                        height: 15,
                      ),
                      Text('Please wait ')
                    ],
                  ),
                )
              : Column(
                  children: [
                    Text("all Songs"),
                    Container(
                      height: 500,
                      child: ListView.builder(
                        itemCount: songsList.length,
                        itemBuilder: (BuildContext context, int index) {
                          return Padding(
                            padding: const EdgeInsets.all(8.0),
                            child: Container(
                              height: 80,
                              width: double.infinity,
                              color: Colors.green,
                              child: Stack(
                                children: [
                                  Padding(
                                    padding: const EdgeInsets.only(
                                        top: 15, left: 15),
                                    child: IconButton(
                                        onPressed: () async {
                                          final player =
                                              AudioPlayer(); // Create a player
                                          final duration = await player.setUrl(
                                              // Load a URL
                                              songsList[
                                                  index]); // Schemes: (https: | file: | asset: )
                                          player.play();
                                        },
                                        icon: Container(
                                            height: 70,
                                            width: 70,
                                            decoration: BoxDecoration(
                                              shape: BoxShape.circle,
                                              color: Colors.black,
                                            ),
                                            child: Icon(
                                              Icons.play_arrow_rounded,
                                              color: Colors.white,
                                            ))),
                                  ),

                                  Align(child: Container(child: Text(songsList[index])))
                                ],
                              ),
                            ),
                          );
                        },
                      ),
                    )
                  ],
                )),
    );
  }

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

  getSongList() async {
    await getSonngCount();
    for (var i = 1; i <= songcount; i++) {
      var songs =
          "https://devshamseer.github.io/all-audio-songs/allsongs/sonng${i}.mp3";
      print(songs);
      songsList.add(songs);

      var seen = Set<String>();
      songsList = songsList.where((songs) => seen.add(songs)).toList();
    }
    setState(() {});
  }
}

  ```
 # End happy hacking 😄
