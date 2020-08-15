<script>
  // your script goes here
  import Flex from "../Layout/Flex.svelte";
  import Card from "../UI/Card.svelte";
  import Task from "../UI/Task.svelte";
  import App from "../App.svelte";

  let newCardCreated = false;
  let newCardTitle = "";
  let newCardInput;
  let kanbanBoard = [
    {
      id: 0,
      name: "To Do",
      tasks: [
        { id: 0, value: "Task 2" },
        { id: 1, value: "Task 3" },
      ],
    },
    {
      id: 1,
      name: "Doing",
      tasks: [{ id: 2, value: "Task 1" }],
    },
    {
      id: 2,
      name: "Testing",
      tasks: [],
    },
    {
      id: 3,
      name: "Done",
      tasks: [],
    },
  ];

  const deleteCard = (id) => {
    console.log("card deleted", id.detail);
  };

  const deleteTask = (id) => {
    console.log("Task deleted", id.detail);
  };

  const moveRight = (id) => {
    console.log("move right", id.detail);
  };

  const moveLeft = (id) => {
    console.log("move left", id.detail);
  };

  function taskBlurred(t) {
    console.log("add tasked blurred");
    // const e = { detail: t.detail.id };
    // t.detail.value === "" ? deleteTask(e) : "";
  }

  function addTask(e, targetValue = "") {
    console.log("add new task");
    // const cardInd = e.target.id.slice(8);
    // const newTaskId = findIdForNewTask();
    // if (cardIsNotEmpty(cardInd)) {
    //   kanbanBoard[cardInd].tasks.push({ id: newTaskId, value: targetValue });
    //   kanbanBoard = kanbanBoard;
    //   // kanbanBoard[cardInd].tasks;
    //   setTimeout(() => {
    //     document.getElementById("t_" + newTaskId).focus();
    //   }, 10);
    // }
  }
</script>

<style>
  /* your styles go here */
</style>

<Flex noWrap={true} align={'start'}>
  {#each kanbanBoard as card, i (card.id)}
    <Card id={'c_' + card.id} title={card.name} on:deleteCard={deleteCard}>
      {#each card.tasks as task, t (task.id)}
        <Task
          id={'t_' + task.id}
          firstCard={i === 0 || kanbanBoard[i].tasks[t].value == ''}
          lastCard={i === kanbanBoard.length - 1 || kanbanBoard[i].tasks[t].value == ''}
          bind:value={kanbanBoard[i].tasks[t].value}
          on:deleteTask={deleteTask}
          on:moveLeft={moveLeft}
          on:moveRight={moveRight}
          on:blurred={taskBlurred} />
      {/each}
      <Flex>
        <button id={'addTask_' + i} on:click={addTask}>+</button>
      </Flex>
    </Card>
  {:else}
    <section>
      <h3>Your board is empty</h3>
      <p>Start adding lists with this button!</p>
      <div id="arrow">→</div>
    </section>
  {/each}

</Flex>
