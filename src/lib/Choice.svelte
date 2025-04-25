<script>
    import { nowIndex } from "../store";
    import { questions } from "../data";

    let { title, myAns = "", correct = ""} = $props()

    const checkAns = () => {
        correct = questions[$nowIndex].correct;
        const obj = questions[$nowIndex].choice
        console.log(title, obj)
        const meclick = Object.keys(obj).find(key => obj[key] === title);
        myAns = meclick
        
    }

</script>

{#if myAns === "" && correct === ""}
<div class="border-2 border-gray-400 my-4 rounded-3xl flex justify-between items-center" onclick={checkAns}>
    <h2 class="p-4"> {title} </h2>
</div>
{:else if myAns === correct}
<div class="border-2 border-green-500 my-4 rounded-3xl flex justify-between items-center bg-green-200 ">
    <h2 class="p-4"> {title}</h2>
    <div class="my-3 mx-5 p-1 rounded-[100%] border-green-500">
        <h1 class="text-green-500"> Correct  </h1>
    </div>
</div>
{:else if myAns !== correct}
<div class="border-2 border-red-500 my-4 rounded-3xl flex justify-between items-center bg-red-200 ">
    <h2 class="p-4"> {title}</h2>
    <div class="my-3 mx-5 p-1 rounded-[100%] border-red-500">
        <h1 class="text-red-500"> Wrong </h1>
    </div>
</div>
{/if}
