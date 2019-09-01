<script>
    import { onMount } from 'svelte';

    let data = [];
    let author = '';
    let quote = '';
    let category = '';


    async function getRandomQuote () {
        const res = await fetch("https://andruxnet-random-famous-quotes.p.rapidapi.com/?cat=famous&count=1", {
            "method": "GET",
            "headers": {
                "x-rapidapi-host": "andruxnet-random-famous-quotes.p.rapidapi.com",
                "x-rapidapi-key": "b88fe7818dmshfb7ded1079f1e6cp1eac4bjsn2398c3270844"
            }
        });
        data = await res.json();
        console.log(data);
        author = data[0].author;
        quote = data[0].quote;
        category = data[0].category;
        console.log(author);
        console.log(quote);
        console.log(category);
    }

    onMount(() => {
        getRandomQuote();
    });

</script>

<svelte:head>
    <!-- font -->
    <link href="https://fonts.googleapis.com/css?family=Chilanka&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Permanent+Marker&display=swap" rel="stylesheet">

    <!-- bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" 
    integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</svelte:head>

<style>
    #btn-generate {
        background: #2C5364;
        font-weight: 600;
        border-radius: 15px;
    }



    .quote-content {
        height: 600px;
        background: #0F2027;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to right, #2C5364, #203A43, #0F2027);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to right, #2C5364, #203A43, #0F2027); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

    }

    p { 
        color: azure;
        font-family: 'Chilanka', cursive;
    }

    p#myquote { 
        
        font-size: 50px;
        font-family: 'Chilanka', cursive;
    }

    p#author {
        font-size: 30px;

    }

    p#category{
        font-size: 25px;
        font-family: 'Permanent Marker', cursive;
    }
    

</style>



<div class="container">

    {#if data.length > 0}
         
         <div class="d-flex justify-content-center py-5 my-2">
            <button id="btn-generate" type="button" class="btn btn-primary p-3" on:click = {getRandomQuote} >Generate New Quote</button>
        </div>

        <div class="quote-content">
            <div class="row justify-content-center">
                <div class="col-md-10 pt-5 my-5">
                    <p id="myquote">"{quote}"</p>
                </div>
            </div>
            <div class="row justify-content-end pt-5 px-2">
                <div class="col-4 pt-3">
                    <p id="author">-{author}</p>
                </div>
            </div>
            <div class="row justify-content-center pt-2">
                <div class="col-4 text-center pt-2">
                    <p id="category">#{category}</p>
                </div>
            </div>
        </div>
        
        
    {:else}
         Loading...
    {/if}

    
    

</div>










