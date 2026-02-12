<script lang="ts">
  import { T } from '@threlte/core'
  import { useTexture } from '@threlte/extras'
  import { SheetObject } from '@threlte/theatre'
  import KeyboardControls from './KeyboardControls.svelte'
  import { cubeGeometry } from './state'

  // Load logo texture
  const logoTexture = useTexture('/finther-img/logo-fintec.png')

  interface Props {
    key: string
  }

  let { key }: Props = $props()
</script>

<SheetObject {key}>
  {#snippet children({ Transform, Sync })}
    <KeyboardControls>
      {#snippet children({ transform })}
        <Transform {...transform}>
          <T.Mesh frustumCulled={false}>
            {#if $cubeGeometry}
              <T
                is={$cubeGeometry}
                dispose={false}
              />
            {/if}
            {#if $logoTexture}
              <T.MeshStandardMaterial
                map={$logoTexture}
                roughness={0.4}
                metalness={0.6}
              >
                <Sync
                  opacity
                  roughness
                  metalness
                />
              </T.MeshStandardMaterial>
            {/if}
          </T.Mesh>
        </Transform>
      {/snippet}
    </KeyboardControls>
  {/snippet}
</SheetObject>
