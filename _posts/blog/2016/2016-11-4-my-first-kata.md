---
categories: [blog]
date: 2016-11-04 10:00:00
layout: post
libraries: [react]
title: "My First Kata"
---

I have been reading a few programming books and they all talked about test-driven development (TDD). I'm pretty new to this discipline and decided it's time for me to learn how to use testing frameworks and test before I write any code. The best way to learn TDD is by doing coding kata. A kata is a exercise that programmers do to train and retain this discipline of test first development. In this blog I will be doing the Roman Numerals Kata in JavaScript.

I will be using <a href="http://blog.coreyhaines.com/2012/12/roman-numerals-kata-with-commentary.html" target="_blank">Roman Numerals Kata with Corey Haines<a/> to help me learn this kata. The testing framework I decided to use is <a href="https://mochajs.org/" target="_blank">Mocha.js</a> and assertion library <a href="http://chaijs.com/" target="_blank">Chai.js</a>.

The importance of TDD is that it allows developers to test the correctness of their code. It's the best way to find bugs and to know when bugs appears. The earlier you spot a bug, the easier it is to fix it. This discipline is about creating test first before writing any code, if you follow this discipline you will write cleaner code. This is my first Kata and I learned a lot about from watching Corey Haines video.

##### Code

{% highlight javascript %}
  "use strict"
  const expect = require('chai').expect;

  function convert(inArabic) {
    if (inArabic <= 0) {
      return '';
    }
    let [arabic, roman] = conversionFactorsFor(inArabic);
    return roman + convert(inArabic - arabic);
  }

  const CONVERSIONS = [
    [1000, "M"],
    [900, "CM"],
    [500, "D"],
    [400, "CD"],
    [100, "C"],
    [90, "XC"],
    [50, "L"],
    [40, "XL"],
    [10, "X"],
    [9, "IX"],
    [5, "V"],
    [4, "IV"],
    [1, "I"]
  ];

  function conversionFactorsFor(inArabic) {
    return CONVERSIONS.find(function(element) {
      return element[0] <= inArabic;
    });
  }

  describe('Converting arabic numbers to roman numerals', function() {
    describe('Roman did not have a 0', function() {
      it('Convert 0 to a empty string', function() {
        expect(convert(0)).to.equal('');
      });
    });

    const arabicToNumerals = {
      1: "I",
      2: "II",
      4: "IV",
      5: "V",
      6: "VI",
      9: "IX",
      10: "X",
      40: "XL",
      50: "L",
      90: "XC",
      100: "C",
      400: "CD",
      500: "D",
      900: "CM",
      1000: "M"
    };

    for (let prop in arabicToNumerals) {
      it(`converts ${prop} to ${arabicToNumerals[prop]}`, function() {
        expect(convert(parseInt(prop))).to.equal(arabicToNumerals[prop]);
      });
    }
  });
{% endhighlight %}

Now to verify this code, you can enter in a Arabic numbers and it will convert it into Roman Numerals below. __Note: the input doesn't allow you to enter in more than five digits__.

<div id="root"></div>

<script type="text/babel">
  $( document ).ready(function() {
    function isNumber(number) {
      return /^\d+$/.test(number);
    }

    function convert(inArabic) {
      if (inArabic <= 0) {
        return '';
      }
      let [arabic, roman] = conversionFactorsFor(inArabic);
      return roman + convert(inArabic - arabic);
    }

    const CONVERSIONS = [
      [1000, "M"],
      [900, "CM"],
      [500, "D"],
      [400, "CD"],
      [100, "C"],
      [90, "XC"],
      [50, "L"],
      [40, "XL"],
      [10, "X"],
      [9, "IX"],
      [5, "V"],
      [4, "IV"],
      [1, "I"]
    ];

    function conversionFactorsFor(inArabic) {
      return CONVERSIONS.find(function(element) {
        return element[0] <= inArabic;
      });
    }

    class Board extends React.Component {
      constructor(props) {
        super(props);
        this.handleChange = this.handleChange.bind(this);
        this.state = {
          value: 123,
          status: convert(123)
        };
      }

      handleChange(e) {
        const value = e.target.value;
        const status = convert(value) || 'Roman did not have a 0'; 
        if (!isNumber(value)) {
          this.setState({
            value: value,
            status: 'You must enter in numbers only'
          });
          return;
        }
        this.setState({
          value: value,
          status: status
        });
      }

      render() {
        return (
          <div className="row">
            <div className="col m4 s8 offset-m4 offset-s2">
              <label>Enter Arabic Number</label>
              <input type="text" value={this.state.value} onChange={this.handleChange} maxLength="5" />
            </div>
            <div className="col m6 s8 offset-m3 offset-s2 center-align">
              <h5>Roman Numerals</h5>
              <p>{this.state.status}</p>
            </div>
          </div>
        );
      } 
    }

    ReactDOM.render(
      <Board />,
      document.getElementById('root')
    );
  });
</script>