<script>
    
    import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher();

	export let editStatus = false;

    export let product = {
        id: "",
        name: "",
        description: "",
        category: "",
        imageURL: "",
    };

    const onSubmitHandler = (e) => {
        /*if (!editStatus){
			addProduct();
		} else {
			UpdateProduct();
		}*/
    };

    function handleEdit(id) {
        dispatch("edit", {
			id : id
		});
    }

</script>

<div class="card">
    <div class="card-body">
        <form on:submit|preventDefault={onSubmitHandler}>
            <div class="form-group">
                <input
                    bind:value={product.name}
                    type="text"
                    placeholder="Product Name"
                    id="product-name"
                    class="form-control"
                />
            </div>
            <div class="form-group">
                <textarea
                    bind:value={product.description}
                    id="product-description"
                    rows="3"
                    placeholder="Product Description"
                    class="form-control"
                />
            </div>
            <div class="form-group">
                <input
                    bind:value={product.imageURL}
                    type="url"
                    id="product-image-url"
                    placeholder="https://faztweb.com/"
                    class="form-control"
                />
            </div>
            <div class="form-group">
                <select
                    id="category"
                    bind:value={product.category}
                    class="form-control"
                >
                    <option value="laptops">Laptops</option>
                    <option value="peripherials">Peripherials</option>
                    <option value="servers">Servers</option>
                </select>
            </div>
            <button class="btn btn-primary" on:click={() => handleEdit(product.id)}>
                {#if !editStatus} Save Product {:else} Update product {/if}
            </button>
        </form>
    </div>
</div>
