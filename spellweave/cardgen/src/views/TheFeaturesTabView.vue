<template>
	<transition name="slide">
		<div class="toolbar-tab tab-features">
			<card-name></card-name>
			<features-card-title-textbox />
			<card-description></card-description>
			<card-tribe></card-tribe>
			<div class="dropdowns">
				<card-element></card-element>
				<card-attack-dropdown />
				<card-health-dropdown />
				<card-initiative-textbox />
				<card-attack-type-dropdown />
			</div>
		</div>
	</transition>
</template>

<script>
	import {Type} from "../util/constant";
	import cardName from '../components/FeaturesCardNameTextbox.vue';
	import cardType from '../components/FeaturesCardTypeDropdown.vue';
	import cardTribe from '../components/FeaturesCardTribeTextbox.vue';
	import isFreeDraw from '../components/FeaturesIsFreeDrawCheckbox.vue';
	import isFreeMove from '../components/FeaturesIsFreeMoveCheckbox.vue';
	import isFreeBuild from '../components/FeaturesIsFreeBuildCheckbox.vue';
	import isPermanent from '../components/FeaturesIsPermanentCheckbox.vue';
	import cardElement from '../components/FeaturesCardElementDropdown.vue';
	import cardPathType from '../components/FeaturesCardPathTypeDropdown.vue';
	import cardGoldCost from '../components/FeaturesCardGoldCostDropdown.vue';
	import cardManaCost from '../components/FeaturesCardManaCostDropdown.vue';
	import cardDescription from '../components/FeaturesCardDescriptionTextbox.vue';
	import CardAttackDropdown from "../components/CardAttackDropdown";
	import CardHealthDropdown from "../components/CardHealthDropdown";
	import CardInitiativeTextbox from "../components/CardInitiativeTextbox";
	import FeaturesCardTitleTextbox from "../components/FeaturesCardTitleTextbox";
	import CardAttackTypeDropdown from "../components/CardAttackTypeDropdown";

	export default {
		components: {
			CardAttackTypeDropdown,
			FeaturesCardTitleTextbox,
			CardInitiativeTextbox,
			CardAttackDropdown,
			CardHealthDropdown,
			cardName,
			cardDescription,
			cardTribe,
			isFreeBuild,
			isFreeDraw,
			isFreeMove,
			isPermanent,
			cardType,
			cardPathType,
			cardElement,
			cardGoldCost,
			cardManaCost,
		},
		computed: {
			isPathTypeVisible() {
				return this.$store.state.cardState.cardType === Type.PATH;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.tab-features {
		.dropdowns {
			display: flex;
			flex-wrap: wrap;
			flex-direction: row;
		}
	}
</style>