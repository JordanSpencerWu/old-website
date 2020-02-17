---
author: Bobby Owsinski
categories: [book]
class: 87
date: 2020-02-15 10:00:00
description: A very useful handbook for mixing engineers. The most important learning for me is timing the delay time to the tempo of the track. This in my opinion gives the track a groove that sounds good, so I created a delay time calculator in my notes for the standard 4/4 time signature.
hidden: true
img-path: /assets/images/books/the-mixing-engineer-handbook.jpg
layout: book
libraries: [mathjax]
permalink: /the-mixing-engineer-handbook/
title: "THE MIXING ENGINEER'S HANDBOOK"
---
#### Mixing Approach

1. Determine the Direction of the Song
2. Develop the Groove
3. Find the Most Important Element and Emphasize It.

#### Rule For Arrangements

1. Limit the number of elements
2. Everything in its own frequency range.

#### Goals of Equalization

1. To make an instrument sound clearer and more defined
2. To make the instrument or mix bigger and larger than life
3. To make all the elements of a mix fit together better by putting each instrument in its own predominate frequency range

tremolo is a cyclic variation in volume

vibrato changes the pitch of the sound.

It's important to time the delay to the track in order for it to pulse with the song.

$1/4\,Note = (60\,Sec\,/\,BPM) * 1000$

$Dotted\,Value = Delay\,Time * 1.5$

$Triplet\,Value = Delay\,Time * (2/3)$

#### Delay Chart (in milliseconds)

<div class="row">
  <div class="input-field col s6 m6 l6">
    <input value="128" id="bpm" type="number" placeholder="Enter a BPM">
    <label class="active" for="bpm">BPM</label>
  </div>
</div>

<div class="row">
  <table class="striped responsive-table">
    <thead id="table-head"></thead>
    <tbody id="table-body"></tbody>
  </table>
</div>

<script type="text/javascript">
  (function() {
    const INPUT_BPM = document.getElementById("bpm");

    INPUT_BPM.onchange = handleBpmChange;

    setUpTable();

    function calculateDelay() {
      const INPUT_BPM = document.getElementById("bpm");
      const bpm = parseInt(INPUT_BPM.value);
      const SECONDS_IN_A_MINUTE = 60;

      let data = {};
      data["BPM"] = bpm;
      data["1/4 Note"] = SECONDS_IN_A_MINUTE / bpm * 1000;
      data["8th Note"] = data["1/4 Note"] / 2;
      data["16th Note"] = data["8th Note"] / 2;
      data["32nd Note"] = data["16th Note"] / 2;
      data["1/4 Triplet"] = data["1/4 Note"] * (2 / 3);
      data["8th Triplet"] = data["8th Note"] * (2 / 3);
      data["16th Triplet"] = data["16th Note"] * (2 / 3);
      data["Dotted 1/4"] = data["1/4 Note"] * 1.5;
      data["Dotted 8th"] = data["8th Note"] * 1.5;
      data["Dotted 16th"] = data["16th Note"] * 1.5;

      return data;
    }

    function setUpTable() {
      const DELAY_INFO = calculateDelay();

      // Table Head
      const TABLE_HEAD = document.getElementById("table-head");
      if (TABLE_HEAD.rows.length > 0) {
        TABLE_HEAD.deleteRow(0);
      }
      const TABLE_HEAD_ROW_0 = TABLE_HEAD.insertRow(0);
      Object.keys(DELAY_INFO).forEach((headerName, index) => {
        let CELL = TABLE_HEAD_ROW_0.insertCell(index);

        CELL.innerHTML = headerName;
      });

      // Table Body
      const TABLE_BODY = document.getElementById("table-body");
      if (TABLE_BODY.rows.length > 0) {
        TABLE_BODY.deleteRow(0);
      }
      const TABLE_BODY_ROW_0 = TABLE_BODY.insertRow(0);
      Object.values(DELAY_INFO).forEach((delay, index) => {
        let CELL = TABLE_BODY_ROW_0.insertCell(index);

        CELL.innerHTML = Number.isInteger(delay) ? delay : delay.toFixed(3);
      });
    }

    function handleBpmChange(event) {
      setUpTable();
    }
  })();
</script>