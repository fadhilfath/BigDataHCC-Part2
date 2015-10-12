# Pokemon

Create interactive visualizations for the Pokemon data. Complete the script
so that when a user clicks on each menu button, there will be a different
bar chart shown in the Viz block.

You will be reusing the code you wrote for generating SVG bar charts a couple weeks
ago. The main challenge is to figure out how to connect your visualization code
with the front-end code (event handlers ... etc).

## Menu

<button id="viz-horizontal">Attack (Horizontal Bars)</button>
<button id="viz-vertical">Attack (Vertical Bars)</button>
<button id="viz-attack-defense">Attack vs. Defense</button>
<button id="viz-speed-defense">Speed vs. Defense</button>
<button id="viz-horizontal-sorted">Attack (sorted from low to high)</button>
<button id="viz-horizontal-sorted-desc">Attack (sorted from high to low)</button>
<button id="viz-attack-speed">Attack (width) vs. Speed (color)</button>

## Viz

<div class="myviz" style="width:100%; height:500px; border: 1px black solid;">
Data is not loaded yet
</div>

{% script %}
// pokemonData is a global variable
pokemonData = 'not loaded yet'

$.get('/data/pokemon-small.json')
 .success(function(data){
     console.log('data loaded', data)
     // TODO: show in the myviz that the data is loaded
     pokemonData = data          
 })


function vizAsHorizontalBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-horizontal').click(vizAsHorizontalBars)


// for each of the TODOs below, you will write a "callback function" similar
// to vizAsHorizontalBars and a $('something').click to add this callback
// function to respond to the click event of a particular button

// TODO: add code to visualize the attack points as a series
// of vertical bars (without labels)

function vizAsVerticalBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(${d.x} ${d.y})"> \
                    <rect   \
                         width="20" \
                         height="${d.height}"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return i * 20
    }

    function computeWidth(d, i) {
        return i * 20 + 20
    }

    function computeHeight(d,i) {
        return d.Attack
    }

    function computeY(d, i) {
        return 0
    }

    function computeColor(d, i) {
        return 'red'
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    height: computeHeight(d,i),
                    color: computeColor(d, i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-vertical').click(vizAsVerticalBars)

// TODO: add code visualize the attack points vs. defense
// points as side-by-side horizontal bar charts (with labels)

function vizAsAttackDefenseBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(120 ${d.y})"> \
                    <rect   \
                         x="-${d.width}" \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <rect   \
                         x="0" \
                         width="${d.width2}" \
                         height="20" \
                         style="fill:${d.color2};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <text x="0" y="13">${d.label}</text> \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Attack
    }

    function computeWidth2(d,i) {
        return d.Defense
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeColor2(d,i) {
        return 'blue'
    }

    function computeLabel(d,i) {
        return d.Name
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    width2: computeWidth2(d,i),
                    color: computeColor(d, i),
                    color2: computeColor2(d,i),
                    label: computeLabel(d,i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-attack-defense').click(vizAsAttackDefenseBars)

// TODO: add code visualize the speed points vs. defense
// points as side-by-side horizontal bar charts (with labels)

function vizAsSpeedDefenseBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(120 ${d.y})"> \
                    <rect   \
                         x="-${d.width}" \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <rect   \
                         x="0" \
                         width="${d.width2}" \
                         height="20" \
                         style="fill:${d.color2};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <text x="0" y="13">${d.label}</text> \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Speed
    }

    function computeWidth2(d,i) {
        return d.Defense
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeColor2(d,i) {
        return 'blue'
    }

    function computeLabel(d,i) {
        return d.Name
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    width2: computeWidth2(d,i),
                    color: computeColor(d, i),
                    color2: computeColor2(d,i),
                    label: computeLabel(d,i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-speed-defense').click(vizAsSpeedDefenseBars)

// TODO: add code to visualize the attack points in ascending order as a
// series of horizontal bar charts (with labels)

function vizAsHorizontalSortedBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <text x="0" y="13">${d.label}</text> \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeLabel(d,i){
        return d.Name
    }

    var viz = _.map(_.sortBy(pokemonData,'Attack'), function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
                    label: computeLabel(d,i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-horizontal-sorted').click(vizAsHorizontalSortedBars)


// TODO: add code to visualize the attack points in descending order as a
// series of horizontal bar charts (with labels)
function vizAsHorizontalSortedDescBars(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <text x="0" y="13">${d.label}</text> \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }
    function computeLabel(d,i) {
        return d.Name
    }

    var viz = _.map(_.sortBy(pokemonData,'Attack').reverse(), function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
                    label:computeLabel(d,i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-horizontal-sorted-desc').click(vizAsHorizontalSortedDescBars)


// TODO: add code to visualize the attack points as a series of horizontal bar
// charts (with labels), and using the brightness of red to represent defense
// points

function vizAsAttackSpeed(){

    // TODO: modify this function to visualize the data as horizontal
    // bars to compare attack points

    // define a template string
    // define a template string
    var tplString = '<g transform="translate(120 ${d.y})"> \
                    <rect   \
                         x="-${d.width}" \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <rect   \
                         x="0" \
                         width="${d.width2}" \
                         height="20" \
                         style="fill:${d.color2};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    \
                    <text x="0" y="13">${d.label}</text> \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {
        return d.Attack
    }

    function computeWidth2(d,i) {
        return d.Speed
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeColor2(d,i) {
            var values = _.pluck(pokemonData,'Speed')
            var maxValue = _.max(values)
            var redValue = ((255/maxValue)) * d.Speed
            return 'rgb(' + redValue + ',0,0)'
        }

    function computeLabel(d,i) {
        return d.Name
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    width2: computeWidth2(d,i),
                    color: computeColor(d, i),
                    color2: computeColor2(d,i),
                    label: computeLabel(d,i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

$('button#viz-attack-speed').click(vizAsAttackSpeed)

{% endscript %}
