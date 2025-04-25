<script>
    import Choice from "$lib/Choice.svelte";
    import { nowIndex } from "../store";
    
    import { questions } from "../data";
    
    let currentIndex = $state(0);
    let currentQuestion = $state(questions[currentIndex])

    const nextQuestion = () =>{
        currentIndex++;
        currentQuestion = questions[currentIndex]
        nowIndex.update(now => now+1)
        
    }

</script>

<section class="h-[100vh] bg-[#420e96] font-mitr flex justify-center items-center">
    <main class="w-[30vw] bg-white p-8 shadow-lg rounded-2xl my-4">
        <h1 class="text-2xl text-gray-400 my-4"> Quiz </h1>
        <p class="text-xl text-shadow-md"> {currentIndex + 1}. {currentQuestion.title}.</p>
        <section class=" my-4">
            
            <Choice title={currentQuestion.choice.A}/>
            <Choice title={currentQuestion.choice.B}/>
            <Choice title={currentQuestion.choice.C}/>
            <Choice title={currentQuestion.choice.D}/>

        </section>

        <div class="flex justify-end p-3">
            <button class="border px-4 py-1 text-white bg-[#420e96] rounded-lg shadow-md" onclick={nextQuestion}> Next </button>
        </div>

    </main>
</section>
