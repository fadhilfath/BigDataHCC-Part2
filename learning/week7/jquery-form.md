# Input

<input id="show" type="text" value="hello"/> <button id="show">Show text</button>

<input id="setcolor" type="text" value="green"/> <button id="setcolor">Set Background Color</button>

<input id="setheight" type="text" value="200"/> <button id="setheight">Set Height</button>

## Bars (1)

<div style="border:1px grey solid; padding:5px;">
Number: <input id="bars1-number" type="text" value="5"/>
<button id="bars1">Show Bars (1)</button>
</div>

## Bars (2)

<div style="border:1px grey solid; padding:5px;">
Number: <input id="bars2-number" type="text" value="5"/>
Color:  <input id="bars2-color" type="text" value="red"/>
<button id="bars2">Show Bars (2)</button>
</div>

## Bars (3)

<div style="border:1px grey solid; padding:5px;">
Number: <input id="bars3-number" type="text" value="5"/>
Color:  <input id="bars3-color" type="text" value="red"/>
Height:  <input id="bars3-height" type="text" value="50"/>
<button id="bars3">Show Bars (3)</button>
</div>


## Viz

<div class="myviz" style="width:100%; height:100px; border: 1px black solid;">
</div>


{% script %}

$('button#show').click(function(){    
    var value = $('input#show').val()    
    console.log(value)
    $('.myviz').html(value)
})

$('button#setcolor').click(function(){    
    // TODO: set the background color of the viz window to the specified color
    var color = $('input#setcolor').val()
    $('.myviz').css('background-color',color)
})

// TODO: add an event handler for "Set Height" button to set the height of the
// viz window to the specified value
$('button#setheight').click(function(){
	var heightVal = $('input#setheight').val()
	$('.myviz').height(heightVal)
})

// TODO: add an event handler for "Show Bars (1)" to display a specified number of
// vertical bars

$('button#bars1').click(function(){
	var numberOfBar = $('input#bars1-number').val()
	var svg = "<svg>"
	console.log('test')
    for(var i = 0;i < numberOfBar;i++){
    	var numX = i * 20 
        svg += "<rect id='rec' height='50' width='10' x='" + numX + "'/>"
    }
    svg += "</svg>"
    $('.myviz').html(svg)   
})

// TODO: add an event handler for "Show Bars (2)" to display a specified number of
// vertical bars in the specified color
$('button#bars2').click(function(){
	var numberOfBar = $('input#bars2-number').val()
	var colorOfBar = $('input#bars2-color').val()
	var svg = "<svg>"
	console.log('test')
    for(var i = 0;i < numberOfBar;i++){
    	var numX = i * 20 
        svg += "<rect id='rec' height='50' width='10' x='" + numX + "'" + "style='fill:" + colorOfBar +"'" + "/>"
    }
    svg += "</svg>"
    $('.myviz').html(svg)   
})

// TODO: add an event handler for "Show Bars (3)" to display a specified number of
// vertical bars in the specified color at the specified height
$('button#bars3').click(function(){
	var numberOfBar = $('input#bars3-number').val()
	var colorOfBar = $('input#bars3-color').val()
	var heightOfBar = $('input#bars3-height').val()
	var svg = "<svg>"
	console.log('test')
    for(var i = 0;i < numberOfBar;i++){
    	var numX = i * 20 
        svg += "<rect id='rec' height='" + heightOfBar + "' width='10' x='" + numX + "'" + "style='fill:" + colorOfBar +"'" + "/>"
    }
    svg += "</svg>"
    $('.myviz').html(svg)   
})

{% endscript %}
