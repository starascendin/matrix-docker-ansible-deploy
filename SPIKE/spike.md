NOTES
- look for `"type":"m.room.message"` for chat messages


EVENT Table
* this has event_id + room_id + ordering, which means this is the essence of the Chat history
* has `sender` user profile id, which should map to event_json message. 

EVENT_JSON
- also has event_id + room_id, but no order and has message + metadata. This is the message content, and should be joined w/ EVENT to for the entire chat

=====
SYNAPSE TABLES

TABLE event_json
- event_id
- room_id - !yHAIJHKxdMRjQwgUKS:aininjas.xyz
- internal_metadata -- {"token_id":5,"device_id":"iMessage Bridge","txn_id":"mautrix-go_1693961348112781000_11"}
- event_json 
	-- {"auth_events":["$dHWImjoTGPmfZImA5JTc7qIMHKt8FhaiuzfcrP8953Y","$zGkgU7A-jfKv73CCu0cvo0xIY7J7ekEgMe1dAv9JLT8","$LpMct2tIFxugNe9ms4lzSnPmjB5u4Ek43pY_OXa_YNg"],"prev_events":["$3J4t8MVGjwcwgGJglDTSzN6zoTAybehB6mh9Dhvi0ZY"],"type":"m.room.message","room_id":"!gfofRKJPWoQpfoszjR:aininjas.xyz","sender":"@whatsapp_19172420128:aininjas.xyz","content":{"body":"And I washed her \nShe hates me","com.beeper.linkpreviews":[],"m.mentions":{},"msgtype":"m.text"},"depth":38,"origin_server_ts":1693006777000,"origin":"aininjas.xyz","hashes":{"sha256":"F2btMktk6gBnnSuSSDC3Nopv3FA1aZdBwYYtGwKR+eM"},"signatures":{"aininjas.xyz":{"ed25519:a_psUz":"zOwsOq5+b+2ovPsOgB/MbHvhUgbS2nTaKGxXeh/MLluayJ07EQSuIc3NeE0CF1Yo6d7XRV3YZqvtwu688m3KDw"}},"unsigned":{"age_ts":1693582989584}}
	-- {"auth_events":["$b5Yqv_m5nQbcqhcWD0whN7bv6pLvdQB9nCX93PhZbi0","$12sn9hXeKNmq0dEXtEerlpMTEVdVRNLcbj4Dieel8b0","$yTjDZLxt64UeuL2_al1iY3W0AncIf40IbWuvd2oIwFs"],"prev_events":["$72E9n3rVRWS49Q7LtPQwCAid93KoEZwurTVze76yrgE"],"type":"m.room.message","room_id":"!yHAIJHKxdMRjQwgUKS:aininjas.xyz","sender":"@bsliu17:aininjas.xyz","content":{"body":"Sooo we going?","fi.mau.double_puppet_source":"mautrix-imessage","fi.mau.imessage.handle":"iMessage;-;+19176646348","fi.mau.imessage.service":"","msgtype":"m.text"},"depth":38,"origin":"aininjas.xyz","origin_server_ts":1693961348237,"hashes":{"sha256":"/FcW56j21HC+WIYQFHq/L99H3WbSxyxDD3nM+I4+zD8"},"signatures":{"aininjas.xyz":{"ed25519:a_psUz":"gW1skOsDAJWJX8kXhCEKJlWh87xpVgSmIGZ9tCGG+jkbhA8CAXmym/GnQG8rGWyqmkoNAAa2zkPonLHnc8OeBw"}},"unsigned":{"age_ts":1693961348237}}
	





TABLE room_stats_state
- room_id --
- name -- (name of the room. This is actually the group, not 1on1)

TABLE room_memberships
(This is a list of events of all room states, which includes:
* bot inviting users to room
* user joins room
)
- event_id
- user_id
- sender
- room_id
- display_name
- membership -- invite/join



# events table
1	topological_ordering	int8	NO	NULL	NULL		NULL
2	event_id	text	NO	NULL	NULL		NULL
3	type	text	NO	NULL	NULL		NULL
4	room_id	text	NO	NULL	NULL		NULL
5	content	text	YES	NULL	NULL		NULL
6	unrecognized_keys	text	YES	NULL	NULL		NULL
7	processed	bool	NO	NULL	NULL		NULL
8	outlier	bool	NO	NULL	NULL		NULL
9	depth	int8	NO	NULL	0		NULL
10	origin_server_ts	int8	YES	NULL	NULL		NULL
11	received_ts	int8	YES	NULL	NULL		NULL
12	sender	text	YES	NULL	NULL		NULL
13	contains_url	bool	YES	NULL	NULL		NULL
14	instance_name	text	YES	NULL	NULL		NULL
15	stream_ordering	int8	YES	NULL	NULL		NULL
16	state_key	text	YES	NULL	NULL		NULL
17	rejection_reason	text	YES	NULL	NULL		NULL


# event_json
1	event_id	text	NO	NULL	NULL		NULL
2	room_id	text	NO	NULL	NULL		NULL
3	internal_metadata	text	NO	NULL	NULL		NULL
4	json	text	NO	NULL	NULL		NULL
5	format_version	int4	YES	NULL	NULL		NULL


# room_stats_state table
1	room_id	text	NO	NULL	NULL		NULL
2	name	text	YES	NULL	NULL		NULL
3	canonical_alias	text	YES	NULL	NULL		NULL
4	join_rules	text	YES	NULL	NULL		NULL
5	history_visibility	text	YES	NULL	NULL		NULL
6	encryption	text	YES	NULL	NULL		NULL
7	avatar	text	YES	NULL	NULL		NULL
8	guest_access	text	YES	NULL	NULL		NULL
9	is_federatable	bool	YES	NULL	NULL		NULL
10	topic	text	YES	NULL	NULL		NULL
11	room_type	text	YES	NULL	NULL		NULL


## Room Model (from FRM hack)
