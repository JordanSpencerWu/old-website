---
categories: [blog]
date: 2016-10-08 10:15:00
layout: post
libraries: [react]
title: "Spotify With React"
---

Spotify provides a RESTful API service that allows developers to access information about artists, albums, and tracks! It's simple to use and most of the time it's not required to have a access token. The only time you need a key and secret is when you access private information like user's profile, playlists, etc. In this blog I created a simple search bar that looks for albums, artists, and tracks with React!

__NOTE__: The search bar below doesn't search as you type, the reason why is there's a API Rate Limits which limits the amount of requests you can make to the API. To use the search bar, type in the album, artist, or track you want to search for then push enter.

<div id="root"></div>

<script type="text/babel">
  $(document).ready(function() {
    class SpotifyContainer extends React.Component {
      constructor(props) {
        super(props);
        this.state = {text: 'Jack Johnson', albums: [], artists: [], tracks: []};
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handleChange = this.handleChange.bind(this);
        this.searchSpotify = this.searchSpotify.bind(this);
        this.addItems = this.addItems.bind(this);
      }

      componentDidMount() {
        this.searchSpotify(this.state.text, this.addItems);
        $('ul.tabs').tabs();
      }

      searchSpotify(query, handleData) {
        $.ajax({
          url: 'https://api.spotify.com/v1/search',
          data: {
            q: query,
            type: 'track,artist,album',
            market: 'US',
            limit: 10
          },
          success: function(response) {
            handleData(response);
          }
        });
      }

      addItems(data) {
        this.setState({
          albums: data.albums.items,
          artists: data.artists.items,
          tracks: data.tracks.items
        });
      }

      handleSubmit() {
        this.searchSpotify(this.state.text, this.addItems);
      }

      handleChange(text) {
        this.setState({text: text});
      }

      render() {
        return (
          <div>
            <Search onHandleSubmit={this.handleSubmit} onHandleChange={this.handleChange} text={this.state.text} />
            <Tabs albums={this.state.albums} artists={this.state.artists} tracks={this.state.tracks} />
          </div>
        );
      }
    }

    class Search extends React.Component {
      constructor(props) {
        super(props);
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handleChange = this.handleChange.bind(this);
      }

      handleSubmit(e) {
        e.preventDefault();
        this.props.onHandleSubmit();
      }

      handleChange(e) {
        this.props.onHandleChange(e.target.value);
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <div className="row">
              <label>Search for Artists, Albums, or Tracks</label>
              <input type="text" value={this.props.text} onChange={this.handleChange} placeholder="Search"/>
            </div>
          </form>
        );
      }
    }

    class Tabs extends React.Component {
      constructor(props) {
        super(props);
      }

      render() {
        return (
          <div className="row">
            <div className="col s12">
              <ul className="tabs">
                <li className="tab col s4"><a href="#albums">Albums</a></li>
                <li className="tab col s4"><a href="#artists">Artists</a></li>
                <li className="tab col s4"><a href="#tracks">Tracks</a></li>
              </ul>
            </div>
            <div id="albums" className="col s12"><Albums albums={this.props.albums} /></div>
            <div id="artists" className="col s12"><Artists artists={this.props.artists} /></div>
            <div id="tracks" className="col s12"><Tracks tracks={this.props.tracks} /></div>
          </div>
        );
      }
    }

    class Albums extends React.Component {
      constructor(props) {
        super(props);
      }

      render() {
        var filterAlbums = this.props.albums.filter(function(album) {
          return album.images[0].url !== undefined;
        });
        return (
          <div class="col s12 m8 offset-m2 l6 offset-l3">
            {filterAlbums.map(function(album) {
              return (
                <div className="card-panel grey lighten-5 z-depth-1">
                  <div className="row valign-wrapper">
                    <div class="col s2">
                      <img width="60" src={album.images[0].url} className="circle responsive-img" /> 
                    </div>
                    <div className="col s10">
                      <a href={'https://open.spotify.com/album/' + album.id} target="_blank">{album.name}</a>
                    </div>
                  </div>
                </div>
              )
            })}
          </div>
        )
      }
    }

    class Artists extends React.Component {
      constructor(props) {
        super(props);
      }

      render() {
        var filterArtists = this.props.artists.filter(function(artist) {
          return artist.images[0] !== undefined;
        });
        return (
          <div class="col s12 m8 offset-m2 l6 offset-l3">
            {filterArtists.map(function(artist) {
              return (
                <div className="card-panel grey lighten-5 z-depth-1">
                  <div className="row valign-wrapper">
                    <div class="col s2">
                      <img width="60" src={artist.images[0].url} className="circle responsive-img" /> 
                    </div>
                    <div className="col s10">
                      <a href={'https://open.spotify.com/artist/' + artist.id} target="_blank">{artist.name}</a>
                    </div>
                  </div>
                </div>
              )
            })}
          </div>
        )
      }
    }

    class Tracks extends React.Component {
      constructor(props) {
        super(props);
      }

      render() {
        return (
          <div class="col s12 m8 offset-m2 l6 offset-l3">
            {this.props.tracks.map(function(track) {
              return (
                <div className="card-panel grey lighten-5 z-depth-1">
                  <div className="row valign-wrapper">
                    <div class="col s2">
                      <img width="60" src={track.album.images[0].url} className="circle responsive-img" /> 
                    </div>
                    <div className="col s10">
                      <a href={'https://open.spotify.com/track/' + track.id} target="_blank">{track.name}</a>
                    </div>
                  </div>
                </div>
              )
            })}
          </div>
        )
      }
    }

    ReactDOM.render(<SpotifyContainer />, document.getElementById('root'));
  });
</script>