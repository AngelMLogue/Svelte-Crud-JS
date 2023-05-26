<script>
    import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher();
    export let product;
    
    function handleDelete(id) {
        dispatch("delete", {
			id : id
		});
    }

    function handleUpdate(id) {
        dispatch("update", {
			id : id
		});
    }

</script>

<div class="card mt-2">
    <div class="row">
        <div class="col-md-4">
            {#if !product.imageURL}
            <img src="images/no-product.png" alt="" class="img-fluid p-2"/>
            {:else}
            <img src="{product.imageURL}" alt="" class="img-fluid p-2">
            {/if}
        </div>
        <div class="col-md-8">
            <div class="card-body">
                <h5>
                    <strong>{product.name}</strong>
                    <span>
                        <small>
                            {product.category}
                        </small>
                    </span>
                </h5>
                <p class="card-text">{product.description}</p>
                <button class="btn btn-danger" on:click={() => handleDelete(product.id)}>
                    Delete
                </button>
                <button class="btn btn-success" on:click={() => handleUpdate(product.id)}>
                    Edit
                </button>
            </div>
        </div>
    </div>
</div>