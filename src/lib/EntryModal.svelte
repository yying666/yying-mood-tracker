<script>
    import supabase from '$lib/db';

    let emojiList = {
   	 worst: '😭',
   	 bad: '🙁',
   	 okay: '😐',
   	 good: '🙂',
   	 best: '😁'
    };

    let emoji = '😐';

    let day = '1';
    let month = '1';
    let year = '2021';
    let mood = 'Okay';
    let comment = 'This is a comment';

    // Insert entry
    async function saveEntry() {
   	 const { error } = await supabase.from('moodEntries').insert(
   		 {
   			 user_id: supabase.auth.user().id,
   			 day: day,
   			 month: month,
   			 year: year,
   			 mood: mood,
   			 comment: comment
   		 }
   	 );
   	 if (error) alert(error.message);

   	 location.reload(); // Refresh the page.
    }
</script>

<div class="modal fade" id="newEntry" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
   	 <div class="modal-content">
   		 <div class="modal-header">
   			 <h5 class="modal-title">New Entry</h5>
   			 <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" />
   		 </div>
   		 <div class="modal-body">
   			 <!-- Date Input -->
   			 <div class="row">
   				 <div class="col">
   					 <form class="form-floating">
   						 <input
   							 type="number"
   							 class="form-control"
   							 id="dayInput"
   							 bind:value={day}
   							 min="1"
   							 max="31"
   						 />
   						 <label for="dayInput">Day</label>
   					 </form>
   				 </div>
   				 <div class="col">
   					 <form class="form-floating">
   						 <input
   							 type="number"
   							 class="form-control"
   							 id="monthInput"
   							 bind:value={month}
   							 min="1"
   							 max="12"
   						 />
   						 <label for="monthInput">Month</label>
   					 </form>
   				 </div>
   				 <div class="col">
   					 <form class="form-floating">
   						 <input
   							 type="number"
   							 class="form-control"
   							 id="yearInput"
   							 bind:value={year}
   							 min="2021"
   						 />
   						 <label for="yearInput">Year</label>
   					 </form>
   				 </div>
   			 </div>

   			 <!-- Mood Scale -->
   			 <div class="row mt-3 text-center">
   				 <h5>How was your day?</h5>
   				 <h1 class="display-1">{emoji}</h1>
   			 </div>
   			 <div class="row px-5">
   				 <div class="btn-group mt-2 mb-3" role="group">
   					 <input
   						 type="radio"
   						 class="btn-check"
   						 name="moodRadio"
   						 id="worst"
   						 autocomplete="off"
   						 on:click={() => {
   							 emoji = emojiList.worst;
   							 mood = 'Worst';
   						 }}
   					 />
   					 <label class="btn btn-outline-danger" for="worst">Worst</label>

   					 <input
   						 type="radio"
   						 class="btn-check"
   						 name="moodRadio"
   						 id="bad"
   						 autocomplete="off"
   						 on:click={() => {
   							 emoji = emojiList.bad;
   							 mood = 'Bad';
   						 }}
   					 />
   					 <label class="btn btn-outline-warning" for="bad">Bad</label>

   					 <input
   						 type="radio"
   						 class="btn-check"
   						 name="moodRadio"
   						 id="okay"
   						 autocomplete="off"
   						 checked
   						 on:click={() => {
   							 emoji = emojiList.okay;
   							 mood = 'Okay';
   						 }}
   					 />
   					 <label class="btn btn-outline-primary" for="okay">Okay</label>

   					 <input
   						 type="radio"
   						 class="btn-check"
   						 name="moodRadio"
   						 id="good"
   						 autocomplete="off"
   						 on:click={() => {
   							 emoji = emojiList.good;
   							 mood = 'Good';
   						 }}
   					 />
   					 <label class="btn btn-outline-info" for="good">Good</label>

   					 <input
   						 type="radio"
   						 class="btn-check"
   						 name="moodRadio"
   						 id="best"
   						 autocomplete="off"
   						 on:click={() => {
   							 emoji = emojiList.best;
   							 mood = 'Best';
   						 }}
   					 />
   					 <label class="btn btn-outline-success" for="best">Best</label>
   				 </div>
   			 </div>

   			 <!-- Comments -->
   			 <div class="form-floating">
   				 <textarea class="form-control" bind:value={comment} id="comment" />
   				 <label for="commentTextarea">Comments</label>
   			 </div>
   		 </div>
   		 <div class="modal-footer">
   			 <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
   			 <button type="button" class="btn btn-primary" on:click={saveEntry}>Add</button>
   		 </div>
   	 </div>
    </div>
</div>