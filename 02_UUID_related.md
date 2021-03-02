1. inserting UUID data type into table

To generate uuid, the extension 'uuid-ossp' needs to be loaded. There are 
several versions of UUID included, common ones are uuid_generate_v5 and 
uuid_generate_v4.

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
do $$
begin
   for cnt in 1000000..1000010 loop
      INSERT INTO test."Results"(id, tags, des)
	  VALUES (uuid_generate_v5('cd374994-1ded-467f-9942-0190af6f5d3a', cnt::TEXT),
			 ARRAY['bb'],
			 'abcabcabc');
   end loop;
end; $$;
select * from test."Results" where not ARRAY['test'] <@ tags;
```
