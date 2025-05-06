| table_schema | table_name        | column_name            | data_type                   | is_nullable | column_default                                  |
| ------------ | ----------------- | ---------------------- | --------------------------- | ----------- | ----------------------------------------------- |
| auth         | audit_log_entries | instance_id            | uuid                        | YES         | null                                            |
| auth         | audit_log_entries | id                     | uuid                        | NO          | null                                            |
| auth         | audit_log_entries | payload                | json                        | YES         | null                                            |
| auth         | audit_log_entries | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | audit_log_entries | ip_address             | character varying           | NO          | ''::character varying                           |
| auth         | flow_state        | id                     | uuid                        | NO          | null                                            |
| auth         | flow_state        | user_id                | uuid                        | YES         | null                                            |
| auth         | flow_state        | auth_code              | text                        | NO          | null                                            |
| auth         | flow_state        | code_challenge_method  | USER-DEFINED                | NO          | null                                            |
| auth         | flow_state        | code_challenge         | text                        | NO          | null                                            |
| auth         | flow_state        | provider_type          | text                        | NO          | null                                            |
| auth         | flow_state        | provider_access_token  | text                        | YES         | null                                            |
| auth         | flow_state        | provider_refresh_token | text                        | YES         | null                                            |
| auth         | flow_state        | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | flow_state        | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | flow_state        | authentication_method  | text                        | NO          | null                                            |
| auth         | flow_state        | auth_code_issued_at    | timestamp with time zone    | YES         | null                                            |
| auth         | identities        | provider_id            | text                        | NO          | null                                            |
| auth         | identities        | user_id                | uuid                        | NO          | null                                            |
| auth         | identities        | identity_data          | jsonb                       | NO          | null                                            |
| auth         | identities        | provider               | text                        | NO          | null                                            |
| auth         | identities        | last_sign_in_at        | timestamp with time zone    | YES         | null                                            |
| auth         | identities        | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | identities        | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | identities        | email                  | text                        | YES         | null                                            |
| auth         | identities        | id                     | uuid                        | NO          | gen_random_uuid()                               |
| auth         | instances         | id                     | uuid                        | NO          | null                                            |
| auth         | instances         | uuid                   | uuid                        | YES         | null                                            |
| auth         | instances         | raw_base_config        | text                        | YES         | null                                            |
| auth         | instances         | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | instances         | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | mfa_amr_claims    | session_id             | uuid                        | NO          | null                                            |
| auth         | mfa_amr_claims    | created_at             | timestamp with time zone    | NO          | null                                            |
| auth         | mfa_amr_claims    | updated_at             | timestamp with time zone    | NO          | null                                            |
| auth         | mfa_amr_claims    | authentication_method  | text                        | NO          | null                                            |
| auth         | mfa_amr_claims    | id                     | uuid                        | NO          | null                                            |
| auth         | mfa_challenges    | id                     | uuid                        | NO          | null                                            |
| auth         | mfa_challenges    | factor_id              | uuid                        | NO          | null                                            |
| auth         | mfa_challenges    | created_at             | timestamp with time zone    | NO          | null                                            |
| auth         | mfa_challenges    | verified_at            | timestamp with time zone    | YES         | null                                            |
| auth         | mfa_challenges    | ip_address             | inet                        | NO          | null                                            |
| auth         | mfa_challenges    | otp_code               | text                        | YES         | null                                            |
| auth         | mfa_challenges    | web_authn_session_data | jsonb                       | YES         | null                                            |
| auth         | mfa_factors       | id                     | uuid                        | NO          | null                                            |
| auth         | mfa_factors       | user_id                | uuid                        | NO          | null                                            |
| auth         | mfa_factors       | friendly_name          | text                        | YES         | null                                            |
| auth         | mfa_factors       | factor_type            | USER-DEFINED                | NO          | null                                            |
| auth         | mfa_factors       | status                 | USER-DEFINED                | NO          | null                                            |
| auth         | mfa_factors       | created_at             | timestamp with time zone    | NO          | null                                            |
| auth         | mfa_factors       | updated_at             | timestamp with time zone    | NO          | null                                            |
| auth         | mfa_factors       | secret                 | text                        | YES         | null                                            |
| auth         | mfa_factors       | phone                  | text                        | YES         | null                                            |
| auth         | mfa_factors       | last_challenged_at     | timestamp with time zone    | YES         | null                                            |
| auth         | mfa_factors       | web_authn_credential   | jsonb                       | YES         | null                                            |
| auth         | mfa_factors       | web_authn_aaguid       | uuid                        | YES         | null                                            |
| auth         | one_time_tokens   | id                     | uuid                        | NO          | null                                            |
| auth         | one_time_tokens   | user_id                | uuid                        | NO          | null                                            |
| auth         | one_time_tokens   | token_type             | USER-DEFINED                | NO          | null                                            |
| auth         | one_time_tokens   | token_hash             | text                        | NO          | null                                            |
| auth         | one_time_tokens   | relates_to             | text                        | NO          | null                                            |
| auth         | one_time_tokens   | created_at             | timestamp without time zone | NO          | now()                                           |
| auth         | one_time_tokens   | updated_at             | timestamp without time zone | NO          | now()                                           |
| auth         | refresh_tokens    | instance_id            | uuid                        | YES         | null                                            |
| auth         | refresh_tokens    | id                     | bigint                      | NO          | nextval('auth.refresh_tokens_id_seq'::regclass) |
| auth         | refresh_tokens    | token                  | character varying           | YES         | null                                            |
| auth         | refresh_tokens    | user_id                | character varying           | YES         | null                                            |
| auth         | refresh_tokens    | revoked                | boolean                     | YES         | null                                            |
| auth         | refresh_tokens    | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | refresh_tokens    | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | refresh_tokens    | parent                 | character varying           | YES         | null                                            |
| auth         | refresh_tokens    | session_id             | uuid                        | YES         | null                                            |
| auth         | saml_providers    | id                     | uuid                        | NO          | null                                            |
| auth         | saml_providers    | sso_provider_id        | uuid                        | NO          | null                                            |
| auth         | saml_providers    | entity_id              | text                        | NO          | null                                            |
| auth         | saml_providers    | metadata_xml           | text                        | NO          | null                                            |
| auth         | saml_providers    | metadata_url           | text                        | YES         | null                                            |
| auth         | saml_providers    | attribute_mapping      | jsonb                       | YES         | null                                            |
| auth         | saml_providers    | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | saml_providers    | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | saml_providers    | name_id_format         | text                        | YES         | null                                            |
| auth         | saml_relay_states | id                     | uuid                        | NO          | null                                            |
| auth         | saml_relay_states | sso_provider_id        | uuid                        | NO          | null                                            |
| auth         | saml_relay_states | request_id             | text                        | NO          | null                                            |
| auth         | saml_relay_states | for_email              | text                        | YES         | null                                            |
| auth         | saml_relay_states | redirect_to            | text                        | YES         | null                                            |
| auth         | saml_relay_states | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | saml_relay_states | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | saml_relay_states | flow_state_id          | uuid                        | YES         | null                                            |
| auth         | schema_migrations | version                | character varying           | NO          | null                                            |
| auth         | sessions          | id                     | uuid                        | NO          | null                                            |
| auth         | sessions          | user_id                | uuid                        | NO          | null                                            |
| auth         | sessions          | created_at             | timestamp with time zone    | YES         | null                                            |
| auth         | sessions          | updated_at             | timestamp with time zone    | YES         | null                                            |
| auth         | sessions          | factor_id              | uuid                        | YES         | null                                            |
| auth         | sessions          | aal                    | USER-DEFINED                | YES         | null                                            |
| auth         | sessions          | not_after              | timestamp with time zone    | YES         | null                                            |
| auth         | sessions          | refreshed_at           | timestamp without time zone | YES         | null                                            |
| auth         | sessions          | user_agent             | text                        | YES         | null                                            |
| auth         | sessions          | ip                     | inet                        | YES         | null                                            |
| auth         | sessions          | tag                    | text                        | YES         | null                                            |