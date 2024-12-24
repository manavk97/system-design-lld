# Spotify

## Understand Requirements

- User can sign up and sign in to the platform.
- User can search for a song.
- User can play a song.
- User can pause a song.
- User can skip a song.
- User can go to the previous song.
- User can go to the next song.
- User can see the current song.
- User can see the list of all the songs.
- User can see the list of all the artists.
- User can see the list of all the albums.
- User can see the list of all the playlists.
- User can see the list of all the podcasts.

## Identify Classes, Objects and Relationships

- **User**: A user of the platform.

```
class User {
  id: string;
  name: string;
  email: string;
  password: string;
}
```

- **Song**: A song in the platform.

```
class Song {
  id: string;
  title: string;
  artist: Artist;
  album: Album;
}
```

- **Playlist**: A playlist in the platform.

```
class Playlist {
  id: string;
  name: string;
  songs: Song[];
}
```

- **Podcast**: A podcast in the platform.

```
class Podcast {
  id: string;
  title: string;
  episodes: PodcastEpisode[];
}
```

- **PodcastEpisode**: A podcast episode in the platform.

```
class PodcastEpisode {
  id: string;
  title: string;
  podcast: Podcast;
}
```

- **Album**: An album in the platform.

```
class Album {
  id: string;
  title: string;
  artist: Artist;
  songs: Song[];
}
```

- **Artist**: An artist in the platform.

```
class Artist {
  id: string;
  name: string;
  songs: Song[];
}
```

- **MusicPlayer**: A music player in the platform.

```
class MusicPlayer {
  id: string;
  user: User;
  currentSong: Song;
  currentPlaylist: Playlist;
  currentPodcast: Podcast;
  currentPodcastEpisode: PodcastEpisode;
}
```

- **MusicStreamer**: A music streamer in the platform.

```
class MusicStreamer {
  id: string;
  user: User;
  musicPlayer: MusicPlayer;
}
```


## Methods

- **User**: A user of the platform.
