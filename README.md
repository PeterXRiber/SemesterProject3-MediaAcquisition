## GraphQL
The GraphQL engine pod runs on this URL: http://lamini1.uvm.sdu.dk:30036/graphql 


## API
Runs on this URL:
http://lamini1.uvm.sdu.dk:31825

### Spotify downloader 

| Path | Method | Input |Description|
| ---- | ------ |-------|-----------|
| / |||Index page for presentations purposes|
| /acquire | POST |`url`: a youtube url|A youtube url that preferable points to a song on YT music, but also works with a normal youtube video. If the youtube-url that is acquired also exists in Spotify, the data and audio-features from Spotify is added to the metadata. The function will acquire all this metadata and store it in the database and it is returned in JSON-format. It also acquires the video-file, when the audio is uploaded, and makes the video available.|


## Youtube downloader
Our youtube downloader pod runs on this URL:
http://lamini1.uvm.sdu.dk:30931

| Path | Method | Input |Description|
| ---- | ------ |-------|-----------|
| / |||Index page for presentations purposes|
| /downloadaudio | POST |`url`: a youtube url|A youtube url that preferable points to a song on YT music, but also works with a normal youtube video|
| /metadata | GET |`url`: a youtube url|Retrieves the metadata from a youtube video or YT music. primary used by us, the complete dataset can retrieves from the GraphQL endpoint|
| /submit | POST |`file`: a .waw file `metadata`: metadata in JSON|Upload your own music and associated metadata formated in JSON, for the right fields look below here|
```
type Artist {
	genres: [String!],
	href: String!,
	id: String!,
	name: String!,
	popularity: Int,
	type: String!,
}

type Album {
	album_type: String!,
	href: String!,
	id: String!,
	name: String!,
	release_date: String!,
	release_date_precision: String!,
	total_tracks: Int!,
	type: String!,
}

type YoutubeTrack {
	abr: Float!,
	acodec: String!,
	album: String,
	alt_title: String,
	artist: String,
	asr: Int!,
	audio_channels: Int!,
	channel: String!,
	creator: String,
	duration: Int!,
	id: String!,
	release_year: Int,
	tags: [String!]!,
	title: String!,
	track: String,
	upload_date: String!
}

type SpotifyTrack {
	album: Album!,
	artists: [Artist!]!,
	disc_number: Int!,
	duration_ms: Int!,
	explicit: Boolean!,
	href: String!,
	id: String!,
	is_local: Boolean!,
	name: String!,
	popularity: Int!,
	preview_url: String,
	track_number: Int!,
	track_type: String!,
}

type AudioFeatures {
	acousticness: Float!,
	analysis_url: String!,
	danceability: Float!,
	duration_ms: Int!,
	energy: Float!,
	id: String!,
	instrumentalness: Float!,
	key: Int!,
	liveness: Float!,
	loudness: Float!,
	mode: Int!,
	speechiness: Float!,
	tempo: Float!,
	time_signature: Int!,
	track_href: String!,
	valence: Float!,
}

type Track {
	_id: String!,
	youtube_data: YoutubeTrack!,
	spotify_data: SpotifyTrack,
	audio_features: AudioFeatures
}
```

