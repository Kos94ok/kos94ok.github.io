<script>
	import {capitalize, formatDateTime, stripMarkup, uuidv4} from "../util/util";

	export default {
		namespaced: true,
		state: {
			data: [],
		},
		getters: {
			getCardById: state => id => {
				for (let i = 0; i < state.data.length; i++) {
					if (state.data[i].id === id) {
						return state.data[i];
					}
				}
				return null;
			},
		},
		mutations: {
			load(state, value) {
				for (let i = 0; i < value.length; i++) {
					state.data.push(value[i]);
				}
			},
			clear(state) {
				state.data.splice(0, state.data.length);
			},
			push(state, value) {
				let item = JSON.parse(JSON.stringify(value));
				item.timestamp = formatDateTime(new Date());

				item.displayName = '';
				if (item.cardName === '') {
					item.displayName = 'Unnamed';
				} else {
					item.displayName = stripMarkup(item.cardName);
				}

				if (item.cardDescription !== '') {
					item.displayName += ': ' + stripMarkup(item.cardDescription);
				}

				let prefix = capitalize(item.cardType);
				if (item.cardElement !== Element.GENERIC) {
					prefix = capitalize(item.cardElement) + ' ' + prefix;
				}
				if (item.cardManaCost > 0) {
					prefix = item.cardManaCost + ' Mana ' + prefix;
				}
				prefix = '[' + prefix + ']';
				item.displayName = prefix + ' ' + item.displayName;

				item.version = 0;
				let library = state.data;
				for (let i = 0; i < library.length; i++) {
					if (library[i].cardName === item.cardName && library[i].version >= item.version) {
						item.version = library[i].version + 1;
					}
				}
				if (item.version > 0) {
					item.displayName += ' (v.' + (item.version + 1) + ')';
				}

				item.id = uuidv4();

				state.data.push(item);
			},
			delete(state, value) {
				let index = state.data.indexOf(value);
				if (index !== -1) {
					state.data.splice(state.data.indexOf(value), 1);
				}
			},
		},
	};
</script>