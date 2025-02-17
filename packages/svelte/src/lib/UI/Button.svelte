<script lang="ts">
	import type { Appearance } from '$lib/types';
	import { generateClassNames } from '@supabase/auth-ui-shared';

	type ButtonProps = svelte.JSX.HTMLAttributes<HTMLButtonElement>;
	type $$Props = Omit<ButtonProps, 'loading'> & {
		loading?: boolean;
		color?: 'default' | 'primary';
		appearance?: Appearance;
	};

	export let color: 'default' | 'primary' = 'default';
	export let appearance: Appearance = {};

	$: classNames = generateClassNames('button', color, appearance);
</script>

<button on:click {...$$restProps} style={appearance?.style?.button} class={classNames.join(' ')}>
	<slot />
</button>

<style>
	button {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 8px;
		border-radius: var(--radii-borderRadiusButton);
		font-size: var(--fontSizes-baseButtonSize);
		padding: var(--space-buttonPadding);
		cursor: pointer;
		border-width: var(--borderWidths-buttonBorderWidth);
		border-style: solid;
		width: 100%;
		transition-property: background-color;
		transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
		transition-duration: 100ms;
	}

	button.default {
		background-color: var(--colors-defaultButtonBackground);
		color: var(--colors-defaultButtonText);
		border-color: var(--colors-defaultButtonBorder);
	}
	button.default:hover {
		background-color: var(--colors-defaultButtonBackgroundHover);
	}

	button.primary {
		background-color: var(--colors-brand);
		color: var(--colors-brandButtonText);
		border-color: var(--colors-brandAccent);
	}
	button.primary:hover {
		background-color: var(--colors-brandAccent);
	}
</style>
