# Alderpen UI

This module adapts the current Cypht application markup to the refreshed Cypht
UI direction without replacing Cypht's PHP output modules or mail behavior.

## Source baseline

- Sanitized fork: `https://github.com/AlderpenGhub/cypht-ui`
- Original UI baseline: `426195da905b6bc052aeeace07ca0e1fd457a3bd`
- Sanitized baseline: `f5f6db196ed3d873635b6fd3108cc629c266db53`
- Local reference: `00-GitClones/cypht-ui`

The original baseline contained an unsafe automatic VS Code task and a
disguised executable payload. Those files were removed from the Alderpen fork
before any UI assets were used. Do not fetch or merge the original upstream
history without reviewing its current security state.

## Integration policy

- Treat the prototype HTML as a visual reference, not production markup.
- Do not import its JavaScript or editor configuration.
- Keep Cypht's existing dynamic controls and accessibility behavior.
- Put local presentation changes in `site.css` so upstream Cypht updates remain
  reviewable.
