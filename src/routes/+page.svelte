<script>
    import Choice from "$lib/Choice.svelte";
    import { nowIndex } from "../store";
    import { questions } from "../data";

    let currentIndex = $state(0);
    let currentQuestion = $state(questions[currentIndex]);
    let correctAns = currentQuestion.correct;
    let score = $state(0);

    let selectedIndex = $state(null);
    let answered = $state(false); // เพิ่มตัวแปรป้องกันการกดซ้ำ
    let eiei = $state(0)

    const checkAns = (index) => {
        eiei += 1;
        if (!answered) {
            selectedIndex = index;
            incrementScore(index); // ส่ง index ที่เลือกเข้าไป
            answered = true;
        }
    };

    const incrementScore = (index) => {
        if (index === correctAns) {
            score += 1;
        }
    };

    const nextQuestion = () => {
        if (currentIndex < questions.length - 1) {
            currentIndex++;
            currentQuestion = questions[currentIndex];
            correctAns = currentQuestion.correct;
            selectedIndex = null;
            answered = false; // รีเซ็ตเมื่อเปลี่ยนคำถาม
        }
    };

    const getOptionClass = (index) => {
        if (selectedIndex === null) {
            return "bg-gray-200 border-gray-500";
        }
        if (index === correctAns) {
            return "bg-green-300 border-green-600";
        }
        if (index === selectedIndex) {
            return "bg-red-300 border-red-600";
        }
        return "bg-gray-200 border-gray-300";
    };
</script>


<section class="h-[100vh] bg-[#420e96] font-mitr flex justify-center items-center">
    <main class="w-[30vw] bg-white p-8 shadow-lg rounded-2xl my-4 max-lg:w-[80vw]">
        
    {#if eiei < 5}
    <div class="flex justify-between">
        <h1 class="text-2xl text-gray-400 my-4"> Quiz </h1>
        <h1 class="text-2xl text-gray-400 my-4"> score = {score} </h1>
    </div>
    
    <p class="text-xl text-shadow-md"> {currentIndex + 1}. {currentQuestion.title}</p>
    
    <section class="my-4">
        {#each currentQuestion.choice as choice, index}
            <div
                class={`border-2 my-4 rounded-3xl flex justify-between items-center cursor-pointer transition-colors duration-300 ${getOptionClass(index)}`}
                on:click={() => {
                    checkAns(index)
                    incrementScore();
                }}
            >
                <h2 class="p-4">{choice}</h2>
                <div class="my-3 mx-5 p-1 rounded-full"></div>
            </div>
        {/each}
    </section>

    <div class="flex justify-end p-3">
        <button class="border px-4 py-1 text-white bg-[#420e96] rounded-lg shadow-md" on:click={nextQuestion}>Next</button>
    </div>
    {:else}
    <h1 class="text-3xl"> Your score is : {score}</h1>
    {/if}
    </main>
</section>
