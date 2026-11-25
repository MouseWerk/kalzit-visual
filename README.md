# kalzit-visual

The approved pictures of Kalzit's screens, for the visual comparison in Kalzit's CI
([MouseWerk/Kalzit](https://github.com/MouseWerk/Kalzit), `ui/e2e/visual.config.ts`).

Every screen of the UI is photographed in light and dark at 360, 1280, 2560 and 3440 px wide (a
set of screens also at 1280 px with twice the device scale) and compared pixel by pixel with the
picture here: `baselines/<width>/<screen>--<theme>.png`. The pictures are made on Linux with
Chromium; fonts are drawn differently on other systems.

They live here and not in Kalzit, so Kalzit's history does not carry every version of about a
thousand pictures. Kalzit names the commit it compares against in `ui/e2e/visual/baselines.lock`
and fetches that commit; this repository is public so CI runners need no secret to fetch it.

## Updating baselines

A change that alters screens on purpose comes as two pull requests:

1. In Kalzit's checkout, with a checkout of this repository beside it:

   ```
   git clone https://github.com/MouseWerk/kalzit-visual.git ../kalzit-visual
   cd ui
   KALZIT_VISUAL_BASELINES=../../kalzit-visual npm run visual:update
   ```

   on Linux (WSL works), or on GitHub's Linux runners with
   `gh workflow run visual.yml --ref <branch> -f update=true` and the artifact
   `visual-baselines` copied into `baselines/`. Only the pictures of screens that changed are
   written; a removed screen's pictures are deleted by hand.
2. A pull request here with the changed pictures, named after the Kalzit pull request.
3. In the Kalzit pull request, `ui/e2e/visual/baselines.lock` set to the commit of that pull
   request here once it is merged.

## Review

The reviewer opens every changed picture in the pull request here (GitHub shows image diffs
side by side, as swipe and as onion skin) and checks that each change is the one the Kalzit pull
request intends. An unintended difference is a bug to fix in Kalzit, never a picture to accept.

## License

AGPL-3.0, like Kalzit (see LICENSE).
