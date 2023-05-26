<script>
	import { update_await_block_branch } from "svelte/internal";
	import Form from "./Form.svelte";
	import Product from "./Product.svelte";
	import { v4 } from "uuid";

	let editStatus = false;

	let currentProduct;

	let products = [
		{
			id: "1",
			name: "HP Pavilion Notebook",
			description: "HP Laptop",
			category: "laptop",
		},
		{
			id: "2",
			name: "Mouse Razer",
			description: "Gaming mouse",
			category: "peropherials",
		},
	];

	const cleanProduct = () => {
		product = {
			id: "",
			name: "",
			description: "",
			category: "",
			imageURL: "",
		};
	};

	const deleteProduct = (event) => {
		products = products.filter((product) => product.id !== event.detail.id);
	};

	const editProduct = event => {
		//currentProduct = products[event.detail.id]
		currentProduct = products.find((product) => product.id === event.detail.id);
		editStatus = true;
	}
	
	const UpdateProduct = (event) => {
			let UpdatedProduct = {
			name: event.detail.name,
			description: event.detail.description,
			id: event.detail.id,
			imageURL: event.detail.imageURL,
			category: event.detail.category
		}
		const productIndex = products.find((product) => product.id === event.detail.id);
		products[productIndex] = UpdatedProduct;
		editStatus = false;
	};

	const addProduct = () => {
		const newProduct = {
			id: v4(),
			name: product.name,
			description: product.description,
			category: product.category,
			imageURL: product.imageURL,
		};

		products = products.concat(newProduct);
		cleanProduct();
		console.log(products);
	};

</script>

<main>
	<div class="container p-4">
		<div class="row">
			<div class="col-md-6">
				{#each products as product}
					<Product {product} on:delete={deleteProduct} on:update={editProduct}/>
				{/each}
			</div>
			<div class="col-md-6">
				<Form product={currentProduct} {editStatus} on:edit={UpdateProduct}/>
			</div>
		</div>
	</div>
</main>
