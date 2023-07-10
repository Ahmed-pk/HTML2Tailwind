<script>

// Using css-to-tailwind-translator 
import { CssToTailwindTranslator } from "css-to-tailwind-translator";

let output = "";

let html = "";

let css = "";

// Function to convert css to tailwindcss
function convert ()
{
    let conversionResult = CssToTailwindTranslator(css, {useAllDefaultValues: true});
    
    let parser = new DOMParser();
    let parsedHtml = parser.parseFromString(html, 'text/html');
  
    conversionResult.data.map( (element) => {
        Array.from(parsedHtml.querySelectorAll(element.selectorName)).map(ele => {
            try {     
                ele.classList.add(...element.resultVal.split(" "));
            } catch (error) {
                
            }
        });
    });

    output = parsedHtml.body.innerHTML;
    
}

</script>

<section class="py-16">
    <div class="container mx-auto flex flex-col gap-6">
        <h1 class="text-5xl text-center font-semibold">HTML2Tailwind</h1>
        
        <div class="flex justify-between gap-6">
            <textarea class="border w-1/2 p-2 outline-none" bind:value={css} cols="30" rows="10" placeholder="Write CSS here"></textarea>
            <textarea class="border w-1/2 p-2 outline-none" bind:value={html} cols="30" rows="10" placeholder="Write HTML here"></textarea>
        </div>
        <button on:click={convert} class="px-6 py-3 bg-slate-600 text-white mx-auto text-xl rounded">Convert</button>

        <h2 class="text-3xl font-semibold">Output:</h2>
        <div class="border">
            {output}
        </div>
    </div>
</section>
