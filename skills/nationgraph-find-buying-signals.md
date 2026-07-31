---
name: Find government buying signals and save them to a list
description: >-
  Search NationGraph for predictive public-sector buying signals, inspect a
  signal and its underlying government sources, then organize the promising ones
  into a working list.
api: openapi/nationgraph-openapi-original.json
auth: HTTP Bearer (Authorization: Bearer <token>)
operations:
  - search_signals_api_v3_signals_search_post
  - get_signal_api_v3_signals__signal_id__get
  - get_signal_data_sources_api_v3_signals__signal_id__sources_get
  - get_lists_api_v3_lists_get
  - create_list_api_v3_lists_post
  - add_signal_to_list_api_v3_lists__list_id__signals__signal_id__post
---

# Find government buying signals and save them to a list

All requests go to `https://api.nationgraph.com` and require an
`Authorization: Bearer <token>` header. Errors return a FastAPI `detail`
envelope (422 for validation failures — read `detail[].loc`).

1. **Search signals.** `POST /api/v3/signals/search`
   (`search_signals_api_v3_signals_search_post`) with your filter/query body.
   Page results with `limit`/`offset`; order with `sort`.
2. **Inspect a signal.** `GET /api/v3/signals/{signal_id}`
   (`get_signal_api_v3_signals__signal_id__get`) to read the full signal.
3. **Check the evidence.** `GET /api/v3/signals/{signal_id}/sources`
   (`get_signal_data_sources_api_v3_signals__signal_id__sources_get`) to see the
   underlying government documents (minutes, budgets, POs, contracts, RFPs).
4. **Get or create a list.** `GET /api/v3/lists` (`get_lists_api_v3_lists_get`);
   if none fits, `POST /api/v3/lists` (`create_list_api_v3_lists_post`).
5. **Add the signal.** `POST /api/v3/lists/{list_id}/signals/{signal_id}`
   (`add_signal_to_list_api_v3_lists__list_id__signals__signal_id__post`). Use
   the batch variant (`batch_add_signals_to_list_...`) for many at once.

No idempotency-key contract is documented — retries on write operations are not
guaranteed idempotent.
