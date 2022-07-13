# Allocation Lifecycles

DRAFT

Allocations are continuously accruing rewards while they're active. Rewards are collected by the indexers, and distributed whenever their allocations are closed. That happens either manually, whenever the indexer wants to force close them, or automatically every maximum 28 epochs - max allocation lifetime (right now, one epoch lasts for \~24h).
