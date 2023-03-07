<script lang="ts">
	import {
		Container,
		Collapse,
		Navbar,
		NavbarToggler,
		NavbarBrand,
		Nav,
		NavItem,
		NavLink,
		Dropdown,
		DropdownToggle,
		DropdownMenu,
		DropdownItem,
		Row,
		Col,
	} from "sveltestrap";
	import Dexie from "dexie";
	import 'bootstrap/dist/css/bootstrap.min.css'
	import type { Table } from "dexie";
	import { Chart, LineSeries } from "svelte-lightweight-charts";

	let isOpen = false;

	function handleUpdate(event){
		isOpen = event.detail.isOpen;
	}

	const toggle = () => (isOpen = !isOpen);
	const data = [
        { time: '2019-04-11', value: 180.01 },
        { time: '2019-04-12', value: 96.63 },
        { time: '2019-04-13', value: 76.64 },
        { time: '2019-04-14', value: 81.89 },
        { time: '2019-04-15', value: 74.43 },
        { time: '2019-04-16', value: 80.01 },
        { time: '2019-04-17', value: 96.63 },
        { time: '2019-04-18', value: 76.64 },
        { time: '2019-04-19', value: 81.89 },
        { time: '2019-04-20', value: 94.43 },
		{ time: '2019-05-11', value: 30.01 },
        { time: '2019-05-12', value: 96.63 },
        { time: '2019-05-13', value: 26.64 },
        { time: '2019-05-14', value: 91.89 },
        { time: '2019-05-15', value: 74.43 },
        { time: '2019-05-16', value: 30.01 },
        { time: '2019-05-17', value: 16.63 },
        { time: '2019-05-18', value: 96.64 },
        { time: '2019-05-19', value: 81.89 },
        { time: '2019-05-20', value: 274.43 },
		{ time: '2019-06-11', value: 80.01 },
        { time: '2019-06-12', value: 96.63 },
        { time: '2019-06-13', value: 76.64 },
        { time: '2019-06-14', value: 111.89 },
        { time: '2019-06-15', value: 84.43 },
        { time: '2019-06-16', value: 40.01 },
        { time: '2019-06-17', value: 96.63 },
        { time: '2019-06-18', value: 76.64 },
        { time: '2019-06-19', value: 11.89 },
        { time: '2019-06-20', value: 84.43 },
		{ time: '2019-07-11', value: 120.01 },
        { time: '2019-07-12', value: 86.63 },
        { time: '2019-07-13', value: 76.64 },
        { time: '2019-07-14', value: 11.89 },
        { time: '2019-07-15', value: 84.43 },
        { time: '2019-07-16', value: 70.01 },
        { time: '2019-07-17', value: 76.63 },
        { time: '2019-07-18', value: 46.64 },
        { time: '2019-07-19', value: 21.89 },
        { time: '2019-07-20', value: 314.43 },
    ]

	//IndexedDB storage wrapper
	//Typescript interface
	interface Docs {
		id?: number;
		name?: string;
		amount?: number;
	}

	class DocsDatabase extends Dexie {
		public docs!: Table<Docs, number>;
		public constructor() {
			super("DocDatabase");
			this.version(1).stores({
				docs: "++id,name,amount",
			});
		}
	}

	const db = new DocsDatabase();
	db.transaction("rw", db.docs, async () => {
		if ((await db.docs.where({ name: "Rocket" }).count()) === 0) {
			const id = await db.docs.add({ name: "Rocket", amount: 69 });

		}
		//const lowDocs = await db.docs.where("docum").below(48).toArray();
	});
  export const sitename: string = 'nylasys'
</script>

<main>
	<Navbar color="dark" dark fixed="top" expand="md" class="navbary" >
		<NavbarBrand href="/">💫nylasys</NavbarBrand>
		<NavbarToggler on:click={() => (isOpen = !isOpen)} />
		<Collapse {isOpen} navbar expand="md" on:update={handleUpdate}>
		  <Nav class="ms-auto" navbar>
			<NavItem>
			  <NavLink href="#about/">About us💞</NavLink>
			</NavItem>
			<NavItem>
			  <NavLink href="#solutions/">Solutions✅</NavLink>
			</NavItem>
			<Dropdown nav inNavbar>
			  <DropdownToggle nav caret>Technology🚀</DropdownToggle>
			  <DropdownMenu end>
				<DropdownItem href="https://github.com/openai/whisper">Whisper</DropdownItem>
				<DropdownItem href="https://github.com/dexie/Dexie.js">Dexie.js</DropdownItem>
				<DropdownItem divider />
				<DropdownItem href="https://github.com/pyscript/pyscript">Pyscript</DropdownItem>
			  </DropdownMenu>
			</Dropdown>
		  </Nav>
		</Collapse>
	</Navbar>
	<Row class='row-fluid'>
		<Col>meow</Col>
    	
	</Row>

	<!-- <py-script>
		from datetime import datetime
		now = datetime.now()
		display(now.strftime("%m/%d/%Y, %H:%M:%S"))
	</py-script> -->
	<Row>
	<Chart width={800} height={600}>
		<LineSeries data={data}/>
	</Chart>
	</Row>
</main>
<style>
	:global(body) {
		padding-top: 60px;
		background: white;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	:navbary {
		padding-inline: 20px;

	}

</style>
